---
title: ångstromCTF - MISC - Shark 2
published: true
---
In this continuation to the Shark 1 challenge, this one will also focus on analyzing packet capture files.

This description for this challenges is as follows... 

![Shark 2 Chall](https://user-images.githubusercontent.com/104336820/168149246-13f1cc23-b9c4-4aef-90b5-12111b395ac5.png)

Looks like their friend hasn't learned to safeguard their traffic better. Let's download the <code class="language-plaintext highlighter-rouge">.pcapng</code> file that is linked in the description and take a peek at what we have.

 
&nbsp;
## Open the file with wireshark-->

![shark2](https://user-images.githubusercontent.com/104336820/168213131-e0d41854-2ca3-4f9e-8b48-59efb39bf7a4.png)



![data filter](https://user-images.githubusercontent.com/104336820/168213216-650a8229-caea-435f-82c3-ccf39f9b9746.png)



![follow stream 2](https://user-images.githubusercontent.com/104336820/168213421-541e78df-12ad-4112-a94e-5e672d6022ff.png)



&nbsp;
## Exporting the data -->

![ASCII](https://user-images.githubusercontent.com/104336820/168213943-85a08240-4faa-41c8-8f2d-1ec1be687956.png)



&nbsp;
## That shark has our flag -->

![shark 2 flag](https://user-images.githubusercontent.com/104336820/168150064-40b092b7-abf4-4002-8d0a-98723b688a29.png)

