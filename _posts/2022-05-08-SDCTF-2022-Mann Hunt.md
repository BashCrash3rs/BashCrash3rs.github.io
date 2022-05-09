---
title: SDCTF 2022 - OSINT - Mann Hunt
published: true
---
This was a really fun OSINT challenge that tasked us with finding someone based on nothing more than a username.

The challenge came with the following description...

We were on the trail of a notorious hacker earlier this week, but they suddenly went dark, taking down all of their internet presence...All we have is a username. We need you to track down their personal email address! It will be in the form <code class="language-plaintext highlighter-rouge">****.sdctf@gmail.com</code>. Once you find it, send them an email to demand the flag!

Username:
mann5549
 
&nbsp;
## First, let's check the username with Sherlock -->

Since all we have is to go off of is a username, we need to leverage it to hone in a bit on our target and maybe some way to pivot onto another clue. The fastest way to get some groundwork laid is to search the username across a large variety of social media sites.

Doing that manually could take a large amount of time so we are going to automate this process with sherlock. To start digging around, we head over to our terminal and use <code class="language-plaintext highlighter-rouge">python3 sherlock mann5549</code>

![sherlock](https://user-images.githubusercontent.com/104336820/167326624-afa7cd75-6698-49e7-badb-6d71abaada85.png)

Sherlock takes the username we give it and runs it against numerous social media websites to determine if the username is found on any of the platforms it checked. After sherlock was done running the username it returns a small list of profiles with that username across a few various sites. This should narrow down our starting point significantly.

As this is a small list of links to go through, we can go ahead and check them out manually. We made our way through the list but stopped on the Twitter account as it caught our attention... 

&nbsp;
## Twitter profile -->

We go ahead and check out a few of them and then we land on the Twitter profile. Immediately upon opening the profile, we can see that this users bio mentions how they set their Twitter account to private because people are after them. 

There are no tweets here but there is here is a link to the users website. 

![mann Twitter](https://user-images.githubusercontent.com/104336820/167339230-c0ef8504-84ef-4075-bebe-f3ec5cc6b22c.png)

&nbsp;
## Mann.code website -->

Pivoting from the Twitter profile, we head over to the website that was linked in the users Twitter profile. 
The homepage of the website doesn't contain much other than a message telling us that the target knows who we are and that we will never find him.

![mann codes homepage](https://user-images.githubusercontent.com/104336820/167343215-25835972-74c2-4cc6-80b4-93a103524966.png)

Before trying anything else, we inspect the website from our Firefox browser by right clicking on the page and selecting Inspect. Within the <code class="language-plaintext highlighter-rouge"><head></head></code> we can see that there is some useful metadata here. We can see a link to github repository

![mann source](https://user-images.githubusercontent.com/104336820/167344934-e39ef41a-4f41-401e-9fe8-70cc3869135b.png)
