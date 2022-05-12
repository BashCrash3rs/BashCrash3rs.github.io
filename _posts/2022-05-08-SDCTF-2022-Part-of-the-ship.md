---
title: San Diego CTF 2022 - OSINT - Part of the ship
published: true
---
This was a super simple OSINT challenge that tasked us with the following...

![Part of the Ship](https://user-images.githubusercontent.com/104336820/167997553-1fa44729-7f0b-4095-b0d0-afd5146279f9.png)

Based on the description, we already have some decent clues to get us heading in the right direction. A few keywords from the description that catch our attention are <code class="language-plaintext highlighter-rouge">memes</code>, <code class="language-plaintext highlighter-rouge">forbidden app</code>, <code class="language-plaintext highlighter-rouge">smiling</code>, and <code class="language-plaintext highlighter-rouge">way back</code>. Even the name of this challenge is nice tip.

The other clue we have that will help us tie everything together is the friends username.

&nbsp;
## Finding the "forbidden app" -->

If you aren't already familiar with the term "the forbidden app" or the phrase "part of the ship", these are references to a specific website for sharing all sorts of memes and other images.

If you didn't already know, a quick Google search of either of those terms will tell you all you need to know. 

The website that these phrases are a reference to is <code class="language-plaintext highlighter-rouge">iFunny.co</code>

&nbsp;
## Searching for the username -->

Trying to figure out how to search the iFunny website for specific usernames will only leave you frustrated. No worries though, we are going to listen to one of the clues we were given in the description and head over to the wayback machine.

Once on the Wayback Machine, we are going to want to search for DannFlashes on the iFunny website.

To do this, we need to know how the website structures the slug in the permalinks. Considering that this is listed as an easy OSINT challenge, we can probably guess at this one and get it right. Likely, we are going to need to include <code class="language-plaintext highlighter-rouge">/user/DanFlashes</code> to the end of the domain name.

![WBDanFlashes](https://user-images.githubusercontent.com/104336820/168002684-dd058cc8-c04a-4204-9a90-e6b925ee60b1.png)

We see that we have one capture for that link from earlier this year. Visiting the snapshot takes us to the profile page for DanFlashes and our flag is waiting there for us...

![DanFlashesProfile](https://user-images.githubusercontent.com/104336820/168003852-9c8919c5-29dc-4387-82d4-37343c1c0490.png)
