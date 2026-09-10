---
title: NNS CTF 2026 - Web Hacker 2
published: true
category: WEB
---


This challenge was a beginner level web exploitation challenge that we thought would be fun to run through. After all, sometimes it is nice to log an easy capture and refresh yourself on some of the basics. We were given a really straight forward challenge introduction that simply asked if we have ever hacked a website before and to start here. It gave us a link to visit:
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/1_Challenge_Intro.webp)
<br><br>

So, we visit the URL and are met with a page that asks us to take a look at the query parameter in the URL and think about how this might be abused by a hacker. The parameter here is <code class="language-plaintext highlighter-rouge">page=1</code>. This should be easy enough as this is what is called an IDOR attack (Insecure Direct Object Reference) and all this kind of attack requires is the simple changing of a URL parameter on a page that is missing an access control check.  
<br><br>

![Challenge Description](/assets/images/NNSCTF2026/3_The_First_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/2_Page_1_URL_Change.webp)
<br><br>

So, all we have to do here is change <code class="language-plaintext highlighter-rouge">page=1</code> to <code class="language-plaintext highlighter-rouge">page=2</code> and that should allow us to move to the next page. We change the parameter and bing, we are able to move on to the next step of the challenge...

## <- IDOR ->

![Challenge Description](/assets/images/NNSCTF2026/4_Page_2_URL.webp)
![Challenge Description](/assets/images/NNSCTF2026/5_IDOR.webp)
<br><br>
