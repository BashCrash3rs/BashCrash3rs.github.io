---
title: BrunnerCTF 2026 - Go Go Decompile
published: true
category: REV
---

An employee at Brunnerne Inc has lost their license key for a program they were using to do some accounting work and needs us to retrieve it for them by decompiling the program that they use called Go Go BudgetMaster. They have given us a .zip file that contains the program we need to dig into. They make mention of using a "magic dragon" program which, of course, is a reference to everyone's favorite decompiler; Ghidra.

![challenge_description](/assets/images/BrunnerCTF/Go-Go-Decompile/Challenge-Description.png)
<br><br>

## <- Let's toss this into Ghidra and see what we're working with ->

Instead of extracting anything from the .zip file, we are just going to throw the whole thing into Ghidra and let it analyze everything to give us a complete lay of the land, so to speak.
<br><br>

![Ghidra analysis](/assets/images/BrunnerCTF/Go-Go-Decompile/Ghidra-Analyze.png)
<br><br>

Ghidra does its analysis and we begin to skim through the output. As we are browsing around, we are initially just looking for keywords that might give us a couple of context clues that we can branch off from. We are basically looking for a starting point so we have a semi-defined path or two to journey down. Whenever you decompile a program, it is a good idea to simply take a minute to take note of things that immediately stand out to you, especially if you already have some idea of what you are looking for. Since this is a CTF challenge, we should probably begin looking for references to a "flag" or some variation of the word. And lo and behold, if we look 
