---
title: BrunnerCTF - Unknown Artist
published: true
category: OSINT
---
This challenge was probably one of the more short and entertaining OSINT challenges that we've tried our hand at recently. The entire vibe here can best be described as a mix of Portal and the @dadfeels YouTube channel. Shoutout to Ha1fdan, the author of this challenge.

An employee at Brunnerne Inc. has made a musical project... but no one actually knows who they are. According to the company, this artist has been using a secret platform to hide a flag and the company has asked us to retrieve it. To help us get started, they have given us a file named osint_unknown-artist.zip

![challenge_description](assets/images/BrunnerCTF/Challenge Description.png)
<br><br>

## <- First, we will take a look at everything the file contains ->

We extract the contents and it contains a file named Brunnerne Inc.mp3 and it is 

Before we run the image file through any of our tools, let's first do <code class="language-plaintext highlighter-rouge">eog tv_chall.jpg</code> to see if we can view the image before proceeding. Our image viewer throws 
an error, telling us that it does not recognize the image as an actual JPEG. 

![eog error](https://user-images.githubusercontent.com/104336820/165018827-0ee7e2c9-7103-478c-b879-91b24dc34044.png)

Of course, we didn't expect it to be as easy as that but nonetheless, it is always a good idea to run down the list of possible avenues to gain any extra info you can.
                
Next, we run some basic tools to get some more technical information about the image we are working with. We put the file through binwalk first with <code class="language-plaintext highlighter-rouge">binwalk -e tv_chal.jpg</code>

![binwalk](https://user-images.githubusercontent.com/104336820/165020194-2a2a0689-4478-4fd9-bf4f-2de5ef113c02.png)

binwalk shows us that there is nothing here to extract. This leads us to believe that maybe we should look at the metadata 
as we now know the flag isn't in a file that we need to extract. The image started life as a TIFF type. Nothing odd here so moving on to try to dig a bit deeper.

We fire up exiftool with <code class="language-plaintext highlighter-rouge">exiftool -v tv_chal.jpg</code> to take a look at the metadata of the file. 
Here we find a couple of things of interest...

![exiftool](https://user-images.githubusercontent.com/104336820/165020443-d386a41f-2448-4eb6-9ff2-6ac16eeab562.png)

exiftool gives us a warning that we have an unknown 30-byte header. Then it proceeds to reset the file type as the header configuration is unrecognized which results in our inability to view the image in its current state. All of our recon has led us to assume that the image itself contains the flag and likely it is a matter of a corrupted header. We likely have ourselves a magic numbers issue.


## <- Fixing the header ->

To take a look at the header we use <code class="language-plaintext highlighter-rouge">hexeditor tv_chal.jpg</code> and immediately we are able to see that the file signature for a JPEG file is not what we have here for the magic numbers. 

![hexeditor](https://user-images.githubusercontent.com/104336820/165021657-cf2d5924-f090-44e5-bf89-538d467d63f1.png)

Let's fix that!

![header fixed](https://user-images.githubusercontent.com/104336820/165021788-104b16c0-89cf-47d2-83b0-679c987cc082.png)

Now that the magic numbers have been corrected, we check <code class="language-plaintext highlighter-rouge">eog tv_chal.jpg</code> again to see if we can view the image now...

![can view](https://user-images.githubusercontent.com/104336820/165021971-5fc73c3a-71a8-49e8-8eeb-bc2ae8cb63bd.png)
