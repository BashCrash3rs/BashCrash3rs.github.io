---
title: NNS CTF 2026 - Web Hacker 2
published: true
category: WEB
---

## <- Multi-Stage IDOR Challenge ->

This challenge was a beginner level web exploitation challenge that we thought would be fun to run through. After all, sometimes it is nice to log an easy capture and refresh yourself on some of the basics. If you're new to web hacking, this type of challenge is all about one of the most common (and easiest to understand) vulnerabilities: IDOR, which stands for Insecure Direct Object Reference.

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

This screen shows us an aircraft boarding pass from an airline called NNS Air. There is a lot of information listed on it but the majority of it is of no use to us other than maybe to confuse us with a bunch of dead ends. One of the first tools that comes to mind when trying to solve web exploits challenges is, of course, Burp Suite. We load up our tool and open the built-in browser option since this browser is already configured to allow traffic to pass through Burp Suite and we will use that browser to visit the page as we might normally (this is the easiest option but you can also configure your own browser in this way instead). Doing so will pass information about the website over to our tool so that we can have a look at the webpage's sitemap. Here we see that we have a couple of endpoints that we can explore. In the <code class="language-plaintext highlighter-rouge">Sitemap</code> tab, we will start to look for anything that looks like it is in reference to our personal data. In this case, we would be looking for references to John (us in this challenge). Flipping through the site map we can see:

> GET /api/boarding-pass/john
<br><br>

![API Endpoints](/assets/images/NNSCTF2026/8_Site_Map_John_Boarding_Pass.webp)
<br><br>


