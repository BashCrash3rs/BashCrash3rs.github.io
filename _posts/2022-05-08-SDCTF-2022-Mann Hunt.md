---
title: SDCTF 2022 - OSINT - Mann Hunt
published: true
---
This was a really fun OSINT challenge that tasked us with finding someone based on nothing more than a username.

The challenge came with the following description...

"We were on the trail of a notorious hacker earlier this week, but they suddenly went dark, taking down all of their internet presence...All we have is a username. We need you to track down their personal email address! It will be in the form <code class="language-plaintext highlighter-rouge">****.sdctf@gmail.com</code>. Once you find it, send them an email to demand the flag!"

Username:
mann5549
 
&nbsp;
## First, let's check the username with Sherlock -->

Since all we have is to go off of is a username, we need to leverage it to hone in a bit on our target and maybe some way to pivot onto another clue. The fastest way to get some groundwork laid is to search the username across a large variety of social media sites.

Doing that manually could take a large amount of time so we are going to automate this process with sherlock. To start digging around, we head over to our terminal and use <code class="language-plaintext highlighter-rouge">python3 sherlock mann5549</code>

![sherlock](https://user-images.githubusercontent.com/104336820/167326624-afa7cd75-6698-49e7-badb-6d71abaada85.png)

Sherlock is a script that takes the username we give it and it runs the name against 300 social media websites to determine if the username is found on any of the platforms it checked. After sherlock was done running the username it returns a small list of profiles with that username across a few various sites. This should narrow down our starting point significantly.

As this is a small list of links to go through, we can go ahead and check them out manually. We made our way through the list but stopped on the Twitter account as it caught our attention... 

&nbsp;
## Twitter profile -->

We go ahead and check out a few of them and then we land on the Twitter profile. Immediately upon opening the profile, we can see that this users bio mentions how they set their Twitter account to private because people are after them. 

There are no tweets here but there is here is a link to the users website. 

![mann Twitter](https://user-images.githubusercontent.com/104336820/167339230-c0ef8504-84ef-4075-bebe-f3ec5cc6b22c.png)

&nbsp;
## Mann.codes website -->

Pivoting from the Twitter profile, we head over to the website that was linked in the users Twitter profile. 
The homepage of the website doesn't contain much other than a message telling us that the target knows who we are and that we will never find him.

![mann codes homepage](https://user-images.githubusercontent.com/104336820/167343215-25835972-74c2-4cc6-80b4-93a103524966.png)

Before trying anything else, we inspect the website from our Firefox browser by right clicking on the page and selecting Inspect. Within the <code class="language-plaintext highlighter-rouge"><head></head></code> tags we can see that there is some useful metadata here. We can see a link to a github repository.

![mannhub source github](https://user-images.githubusercontent.com/104336820/167346888-4c10310d-c9f8-48d0-bdd5-37d3c4d570eb.png)

&nbsp;
## Pivoting to the Github repo -->

Following the link we found tucked away in the source code of the website, we end up on the Github repository owned by our target...

![mann repo](https://user-images.githubusercontent.com/104336820/167347902-c2032635-9043-47e8-b2f3-6e1ee949c0fe.png)

We can see that a couple of things have been deleted, again, due to our target knowing that they are being tracked down.

If we click on the description for the <code class="language-plaintext highlighter-rouge">src</code> folder we are taken to the page that shows us all of the commits made by our target. There are a total of 6 files here that have been changed. One of those is labeled <code class="language-plaintext highlighter-rouge">gatsby-config.js</code>:

![repo commits](https://user-images.githubusercontent.com/104336820/167350767-e21fc948-5706-4249-9ff2-55e247b18ce9.png)

If we expand this section to see further up the file, we find a summary that reads "Blogger and Coder for ACM at UC San Diego". 

![expanded changes](https://user-images.githubusercontent.com/104336820/167351507-f0c55c47-383b-4239-a293-47c1908c7e4c.png)

We decide to just keep it simple and put our amazing Google skills to work and the first result matches our query and goes to a LinkedIn account for an Emanuel Hunt.

&nbsp;
## LinkedIn -->

![linkedin](https://user-images.githubusercontent.com/104336820/167351648-03c0223d-968b-4d4d-8524-2b1c838962e8.png)

In the "About" section of our target's LinkedIn page we are given a link to download his resume. We visit the link to look at his resume and notice that the email we need to retrieve has been replaced with asteriks. 

&nbsp;
## Got the credentials -->

![resume1](https://user-images.githubusercontent.com/104336820/167353216-9460ecb5-5a6b-40c3-8eb0-5b8c47c0fd92.png)

Luckily for us, in the right-hand panel under the sharing section we can hover over our targets profile and it displays their email address.

![mannemail](https://user-images.githubusercontent.com/104336820/167353059-de10f7a2-d40f-4e79-bfc1-b934b8af552d.png)




