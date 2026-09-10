---
title: NNS CTF 2026 - Web Hacker 2
published: true
category: WEB
---

***THIS CTF WRITEUP IS IN PROGRESS**

This challenge was a beginner level web exploitation challenge that we thought would be fun to run through. After all, sometimes it is nice to log an easy capture and refresh yourself on some of the basics. We were given a really straight forward challenge introduction that simply asked if we have ever hacked a website before and to start here. It gave us a link to visit:
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/1_Challenge_Intro.webp)
<br><br>

We visit the URL and are met with a page that asks us to take a look at the query parameter in the URL and think about how this might be abused by a hacker. The parameter here is <code class="language-plaintext highlighter-rouge">page=1</code>. This should be easy enough as this is what is called an IDOR attack (Insecure Direct Object Reference) and all this kind of attack requires is the simple changing of a URL parameter on a page that is missing an access control check.  
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/3_The_First_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/2_Page_1_URL_Change.webp)
<br><br>

So, all we have to do here is change <code class="language-plaintext highlighter-rouge">page=1</code> to <code class="language-plaintext highlighter-rouge">page=2</code> and that should allow us to move to the next page. We change the parameter and are able to move on to the next step of the challenge...
<br><br>

## <- IDOR ->

![Challenge Description](/assets/images/NNSCTF2026/4_Page_2_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/5_IDOR.webp)
<br><br>

Once we land on page 2 we are met with the above screen. It tells us:

> "To retrieve the flag, you'll need to take this attack a step further. The <code class="language-plaintext highlighter-rouge">admin</code> user may have something interesting waiting for you."

In that quote, the name admin is highlighted in a way that is sort of hard to ignore! This likely wasn't going to just be a subtle hint at anything more elaborate and it isn't a simple placeholder for some other name that we need to go searching for, it is a direct and intentional reference to the username <code class="language-plaintext highlighter-rouge">admin</code>. This is something we take note of and continue on to now perform a little bit of recon to see what else we are working with here.
