---
title: ångstromCTF - Misc. - Confetti
published: true
---
&nbsp;

For this challenge we were given an image of confetti and the lyrics to the song Confetti by Little Mix: "From the sky, drop like confetti All eyes on me, so V.I.P All of my dreams, from the sky, drop like confetti"

![Confetti snap](https://user-images.githubusercontent.com/104336820/167222509-53cfd4d5-a8c8-40ac-9438-07b1aa569e6d.png)
<br><br>

## <- Do your thing, binwalk ->

We passed the image through binwalk first to see if there was anything else attached to the file. Going back to the lyrics we were given for the description of this challenge, it mentions confetti dropping from the sky. Reminds us of a certain binwalk argument that looks like a star falling from the sky: <code>binwalk --dd ".*" confetti.png</code>

![binwalk-stars](https://user-images.githubusercontent.com/104336820/167224259-8fbff8f7-b7e5-43c2-9a09-6f58c0fd518c.png)

Now that we can see that there is more here than just the single image of confetti, it is likely that our flag is hanging out somewhere in that data. Let's take a look...

![Confetti extracted](https://user-images.githubusercontent.com/104336820/167224799-15357ef1-b4a9-48a7-966d-3341a61fa531.png)

![Confetti extracted folder](https://user-images.githubusercontent.com/104336820/167224835-b0acd030-8e89-4c1c-b6f9-27d1065e5ddd.png)

Sitting in the extracted folder we can see what appears to be a flag in the center of one of the images. Clicking into it, and we are able to capture the flag.

![Confetti Flag](https://user-images.githubusercontent.com/104336820/167224949-8f91dae5-b5ba-428f-b240-8605828ea4ca.png)
