---
title: NNS CTF 2026 - Web Hacker 2
published: true
category: WEB
---

## <- Multi-Stage IDOR Challenge ->

This challenge was a beginner level web exploitation challenge that we thought would be fun to run through. After all, sometimes it is nice to log an easy capture and refresh yourself on some of the basics. If you're new to web hacking, this type of challenge is all about one of the most common (and easiest to understand) vulnerabilities: <code class="language-plaintext highlighter-rouge">IDOR</code>, which stands for <code class="language-plaintext highlighter-rouge">Insecure Direct Object Reference</code>.

Basically, IDOR exploitation is what happens when a website lets you look at someone else's stuff just by changing a piece of the web address (URL), because the server never actually checks whether you're allowed to see it. This is a type of access control vulnerability.

Jumping into this challenge, we were given a really straight forward introduction that simply asked if we have ever hacked a website before and to start here. It gave us a link to visit:
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/1_Challenge_Intro.webp)
<br><br>

## <- Pagination IDOR ->

We visit the URL and are met with a page that asks us to take a look at the query parameter in the URL and think about how this might be abused by a hacker. The parameter here is <code class="language-plaintext highlighter-rouge">page=1</code>. This step of the challenge is what we might refer to as pagination IDOR since right now what we are dealing with is simply hopping from one page to the next by manipulating the URL.
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/3_The_First_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/2_Page_1_URL_Change.webp)
<br><br>

So, all we have to do here is change <code class="language-plaintext highlighter-rouge">page=1</code> to <code class="language-plaintext highlighter-rouge">page=2</code>. We change the parameter and are able to move on to the next step of the challenge...
<br><br>

## <- Taking things a step further ->

![Challenge Description](/assets/images/NNSCTF2026/4_Page_2_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/5_IDOR.webp)
<br><br>

Once we land on page 2 we are met with the above screen. It tells us:

> "To retrieve the flag, you'll need to take this attack a step further. The <code class="language-plaintext highlighter-rouge">admin</code> user may have something interesting waiting for you."
<br><br>

## <- Watching what the website is doing behind the scenes ->

In that quote, the name 'admin' is highlighted in a way that is sort of hard to ignore! This likely wasn't going to just be a subtle hint at anything more elaborate and it isn't a simple placeholder for some other name that we need to go searching for, it is a direct and intentional reference to the username <code class="language-plaintext highlighter-rouge">admin</code>. This is something we take note of and continue on to now perform a little bit of recon to see what else we are working with here. In order to begin doing that, we are going to clock on the "Go to challenge" link that we've been given. Before we decided to use that link, we went ahead and tested the changing of the page number again to <code class="language-plaintext highlighter-rouge">page=3</code> and even <code class="language-plaintext highlighter-rouge">page=4</code> just to be thorough moreso than expecting to find something else. You never really know what you might stumble across and it never hurts to keep exploring just a little bit further, especially if it only takes a few seconds to do it. Of course, we didn't find anything else by doing this so we went ahead and opened up the link that was provided to us for advancing to the next step of the challenge. When we open it up, we are met with the following screen:
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/6_Boarding_Pass.webp)
<br><br>

This screen shows us an aircraft boarding pass from an airline called NNS Air. There is a lot of information listed on it but the majority of it is of no use to us other than maybe to confuse us with a bunch of dead ends. One of the first tools that comes to mind when trying to solve web exploits challenges is, of course, Burp Suite. We load up our tool and open the built-in browser option since this browser is already configured to allow traffic to pass through Burp Suite and we will use that browser to visit the page as we might normally (this is the easiest option but you can also configure your own browser in this way instead). Doing so will pass information about the website over to our tool so that we can have a look at the webpage's sitemap. Here we see that we have a couple of endpoints that we can explore. In the <code class="language-plaintext highlighter-rouge">Sitemap</code> tab, we will start to look for anything that looks like it is in reference to our personal data. In this case, we would be looking for references to John as this is the name we can see on the boarding pass (us in this challenge). Flipping through the site map we can see:

> GET /api/boarding-pass/john
<br><br>

![API Endpoints](/assets/images/NNSCTF2026/8_Site_Map_John_Boarding_Pass.webp)
<br><br>

If we click on that request, we will see the raw data that the server sent back to us in <code class="language-plaintext highlighter-rouge">Response</code> panel. What we find there is a chunk of JSON (structured text data) that looks like this:
<br><br>

![API Endpoints](/assets/images/NNSCTF2026/7_BurpSuite_Intercept_JSON.webp)
<br><br>

The most important part of that JSON chunk for us is right near the top:

>{
>   "id": "01d6fcce-1d70-7000-af8e-08b834415b5a",
>   "username": "john",
>   "qrCode": "..."
>}

Right there in the chunk we see the username <code class="language-plaintext highlighter-rouge">John</code>. So this poses one important question to us... what if we were to change that name somehow and send the request back?

Now, before we just take a guess at this being the solution we are looking for, let's take a minute to see what is actually happening here. If we just do <code class="language-plaintext highlighter-rouge">View Page Source</code> on the webpage or look deeper into the Response body of the page's own load request in Burp Suite, we will find the following JavaScript buried in there:

> // You are signed in as john.
> const username = 'john';
> fetch('/api/boarding-pass/' + username)

What this tells us is that we have pretty much found the smoking gun. The website's own front-end code has our username hardcoded and uses it to ask the server for our boarding pass. There's no login token or session check that's happening here, it's just building a URL with a name and sending it. This means that the server is trusting whatever name shows up in that URL, all with no questions asked. The key takeaway here is that if a website builds a request to fetch "your" data using a plain, visible identifier (a name, a number, an ID) instead of relying on something tied to your actual login session, you can usually just... ask for someone else's identifier instead.
<br><br>

## <- Trying the wrong guess ->

Any hacker worth their weight will typically try out various avenues in an attempt to learn what a system or platform is doing and why, and this often includes going so far as to try things that they already have a good idea simply won't work. And that is exactly what we did next. We have a pretty good idea of how to solve this challenge but still decided to go ahead and try out another angle first. We decided to try to use the the internal ID found in that chunk of JSON from before. That long string of letter and numbers is also what is called a Universally Unique Identifier (UUID). 

**Fun fact:** A UUID is a 128-bit number that is used to identify information in computer systems and is typically written as a 36-character string of letters and numbers separated by hyphens.

To do this, we right-click the original request and choose <code class="language-plaintext highlighter-rouge">Send to Repeater</code>:

> GET /api/boarding-pass/john

We then click into the Repeater tab (this tool is for manually editing a request and re-sending it as many times as you'd like) and just change the name john with the UUID like this:

> GET /api/boarding-pass/01d6fcce-1d70-7000-af8e-08b834415b5a

We click Send and the Response we get back is a <code class="language-plaintext highlighter-rouge">404 Not Found</code> error. This is perfectly fine because this lets us know that the server only accepts usernames in that spot, not any kind of ID. Every failed guess should teach you something about how the system works. This should illustrate the fact that you should never get discouraged by making a wrong turn; making mistakes or following bad leads ultimately just narrows things down for you. The entire reason we enjoy doing CTFs is simply for the love of learning how various tech works. Leaderboards are nice and all, but they are meaningless if you don't actually learn anything in the process or understand how things work under the hood. Fail harder and fail often... it will make you a better hacker.
<br><br>

## <- The flag ->

The same way that we tested out the wrong turn is exactly the same method we will use to retrieve the flag. Except this time instead of using the UUID, we will use the username that the challenge mentioned to us: <code class="language-plaintext highlighter-rouge">admin</code>:

> GET /api/boarding-pass/admin HTTP/2

We now just click Send and check out the Response we get back. We received a <code class="language-plaintext highlighter-rouge">200 OK</code> which means that is was a success. Embedded in one of the fields (the destination city name) was our flag:
<br><br>

![flag](/assets/images/NNSCTF2026/10_Response_and_Flag.webp)
<br><br>

> Here is our flag! <code class="language-plaintext highlighter-rouge">NNS{You_aR3_NOw_1337_H4cker_1NDe3D}</code>

## <- What actually made this vulnerable ->

Think of it like a hotel where your room key also happens to work on every other door in the building, and the front desk never checks whether the key you're holding matches the room you're trying to enter. The server had a rule like "whatever username shows up in the URL, hand back that user's data"  ...but it never asked "wait, is the person asking actually allowed to see this information?"

That's the whole bug. No cleverness needed beyond simply noticing the pattern and then testing it.
<br><br>

## <- How to spot this kind of bug yourself ->

Ask yourself these questions whenever you're testing a website:

- Does any URL or request contain a name, number, or ID that clearly refers to "me" or "my data"? (A username, an account number, an order ID, etc, etc, etc.)
- What happens if I change that value to something else? Perhaps another user's name, a nearby number, a different ID?
- Does the server check who I actually am (via login session/cookie) before handing back data, or does it just trust whatever's in the URL?

If the answer is the last point is "it just trusts the URL," well, then you've likely found an IDOR.
<br><br>

## <- Tools Used ->

- Burp Suite (Community Edition, free) - to intercept and replay web requests
   - Proxy / Site map - to see what requests the page makes
   - Repeater - to manually edit and re-send a request as many times as you want, and see the response instantly
<br><br>

## <- Key takeaways for beginners ->

- IDOR is one of the simplest vulnerabilities to understand and one of the most common in real-world web apps; a great first one to master.
- Always check a page's front-end JavaScript/HTML source. It often reveals exactly how the app decides what data to ask for, including hardcoded values you can manipulate.
- A "wrong guess" (like trying the UUID first) isn't wasted effort. It teaches you something about how the target actually works and gets you closer to the right approach.
- Read challenge hints literally before assuming they're a puzzle. Sometimes "the admin user" really does just mean: try the word <code class="language-plaintext highlighter-rouge">admin</code>.
