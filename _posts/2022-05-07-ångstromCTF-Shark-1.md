---
title: SDCTF 2022 - MISC - Shark 1
published: true
---
This was a fairly simple wireshark packet analysis challenge. For this challenge, we were given the following description:

![Shark 1 Chall](https://user-images.githubusercontent.com/104336820/167767148-70c0e033-03cb-4a02-93d8-cf79c1b5b6ef.png)

We were given a link to download a PCAPNG file. This is the file that we will need to examine in order to retrieve our flag. 
 
&nbsp;
## Open the file with wireshark-->

Since this is a packet capture file, we will go ahead and open it up with wireshark. In the packet list pane, we have a lot of packets displayed.

![Shark1](https://user-images.githubusercontent.com/104336820/167744574-5f409363-ca4a-4e56-a17d-e0186ce3f496.png)

We aren't going to need all of these as we already have a hint as to what we are looking for. We can go ahead and narrow our search down to only TCP protocol using the filter toolbar...

![tcp filter](https://user-images.githubusercontent.com/104336820/167768353-ea300580-ae3c-4881-83ac-45ed74dd10aa.png)

&nbsp;
## Follow the stream-->




