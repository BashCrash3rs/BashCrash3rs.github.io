---
layout: default
title: About Me // Terminal
---

Your existing Markdown content goes here. All of your original text, paragraphs, lists, and headings will remain completely intact right here.

<!-- ================= START OF TERMINAL WIDGET ================= -->
<style>
    .custom-terminal {
        background-color: #050505 !important;
        color: #00ff33 !important;
        font-family: 'Courier New', Courier, monospace !important;
        padding: 30px;
        margin: 20px auto;
        line-height: 1.6;
        font-size: 18px;
        border-radius: 6px;
        border: 1px solid #222;
        box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        max-width: 800px;
        width: 100%;
        box-sizing: border-box;
    }
    .custom-terminal .cursor {
        display: inline-block;
        width: 10px;
        height: 1.2em;
        background-color: #00ff33;
        margin-left: 2px;
        vertical-align: middle;
        animation: terminal-blink 0.8s infinite;
    }
    @keyframes terminal-blink {
        0%, 49% { background-color: #00ff33; }
        50%, 100% { background-color: transparent; }
    }
    .custom-terminal .matrix-text {
        text-shadow: 0 0 5px rgba(0, 255, 51, 0.5);
        white-space: pre-wrap; 
    }
</style>

<div class="custom-terminal">
    <span id="typewriter" class="matrix-text"></span><span class="cursor">&nbsp;</span>
</div>

<script>
    const aboutText = `> OBTAINING CREDENTIALS...\n> ACCESS GRANTED...\n> INITIALIZING TEAM PROFILE...\n\nName: BashCrash3rs \nSpecs: Web / Rev / Pwn / OSINT / Steg \n\nBIOGRAPHY:\nWe are a CTF team based in Houston, Texas. This is our official website, our quaint little corner of the interwebz where we host our CTF writeups and maybe a few other things here and there. When not competing in a CTF, we are usually auditing code, configuring networks, and converting caffeine into clean syntax.\n\nWe ba$h. We cr4sh. Sometimes we even cr4sh on the ba$h.\n\n> STATUS: ONLINE. READY FOR COLLABORATION.`;

    const speed = 40; 
    const initialDelay = 1500; 
    let index = 0;
    
    document.addEventListener("DOMContentLoaded", function() {
        const targetElement = document.getElementById("typewriter");
        if (!targetElement) return;

        function typeWriter() {
            if (index < aboutText.length) {
                targetElement.textContent += aboutText.charAt(index);
                index++;
                setTimeout(typeWriter, speed);
            }
        }
        setTimeout(typeWriter, initialDelay);
    });
</script>
<!-- ================= END OF TERMINAL WIDGET ================= -->

You can also continue writing normal Markdown down here, below the terminal. This text will also render normally using your original background and theme layout.
