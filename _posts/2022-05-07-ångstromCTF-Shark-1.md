---
title: ångstromCTF - MISC - Shark 1
published: true
---
This was a fairly simple wireshark packet analysis challenge. For this challenge, we were given the following description:

![Shark 1 Chall](https://user-images.githubusercontent.com/104336820/167767148-70c0e033-03cb-4a02-93d8-cf79c1b5b6ef.png)

We were given a link to download a PCAPNG file. This is the file that we will need to examine in order to retrieve our flag. 
 
&nbsp;
## Open the file with wireshark-->

Since this is a packet capture file, we will go ahead and open it up with wireshark. In the packet list pane, we have a lot of packets displayed.

![Shark1](https://user-images.githubusercontent.com/104336820/167744574-5f409363-ca4a-4e56-a17d-e0186ce3f496.png)

We aren't going to need all of these as we already have a hint as to what we are looking for. We can go ahead and narrow our search down to only <code class="language-plaintext highlighter-rouge">TCP</code> protocol using the filter toolbar...

![filter results](https://user-images.githubusercontent.com/104336820/167771744-f6d47e54-8a7e-40bb-a986-150825e4d438.png)

Now that we have our results filtered, let's scroll through a few of the packets in the list and pay attention to packet bytes pane for anything that may give us some more information about what is being passed in these packets.

As we scroll through, we land on one that gives us some plaintext regarding the flag.

![tcp filter](https://user-images.githubusercontent.com/104336820/167768353-ea300580-ae3c-4881-83ac-45ed74dd10aa.png)

&nbsp;
## Follow the stream-->

Since we know the packets contain plaintext, we can just right click on the packet and select <code class="language-plaintext highlighter-rouge">follow stream</code> and it will give it all to us in a readable format.

And there is our flag...

![follow stream](https://user-images.githubusercontent.com/104336820/167770895-c90a1913-8073-4576-a93b-99a1d79e982a.png)

