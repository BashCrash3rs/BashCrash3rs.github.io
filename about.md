---
layout: Page
title: About Me // Terminal
---

<style>
    /* Terminal background and font setup */
    .terminal-body {
        background-color: #050505;
        color: #00ff33;
        font-family: 'Courier New', Courier, monospace;
        padding: 40px;
        margin: 0;
        line-height: 1.6;
        font-size: 18px;
    }

    /* Container to keep content centered and readable */
    .terminal-container {
        max-width: 800px;
        margin: 0 auto;
    }

    /* The blinking cursor effect */
    .cursor {
        display: inline-block;
        width: 10px;
        background-color: #00ff33;
        margin-left: 2px;
        animation: blink 0.8s infinite;
    }

    @keyframes blink {
        0%, 49% { background-color: #00ff33; }
        50%, 100% { background-color: transparent; }
    }

    /* Matrix-like subtle text glow */
    .matrix-text {
        text-shadow: 0 0 5px rgba(0, 255, 51, 0.5);
        white-space: pre-wrap; /* Preserves line breaks from the script */
    }
</style>

<div class="terminal-body">
    <div class="terminal-container">
        <!-- The text will type out inside this span -->
        <span id="typewriter" class="matrix-text"></span><span class="cursor">&nbsp;</span>
    </div>
</div>

<script>
    // Define the about page text here. Use \n for new lines.
    const aboutText = `> OBTAINING CREDENTIALS...\n> ACCESS GRANTED...\n> INITIALIZING TEAM PROFILE...\n\nName: BashCrash3rs \nSpecs: Web / Rev / Pwn / OSINT / Steg \n\nBIOGRAPHY:\nWe are a CTF team based in Houston, Texas. This is our official website, our quaint little corner of the interwebz where we host our CTF writeups and maybe a few other things here and there. When not competing in a CTF, we are usually auditing code, configuring networks, and converting caffeine into clean syntax.\n\nWe ba$h. We cr4sh. Sometimes we even cr4sh on the ba$h.\n\n> STATUS: ONLINE. READY FOR COLLABORATION.`;

    const speed = 40; // Typing speed in milliseconds per character (lower is faster)
    const initialDelay = 1500; // How long to wait (in milliseconds) before typing starts
    let index = 0;
    
    // Using a scoped DOMContentLoaded event listener ensures this fires properly inside Jekyll templates
    document.addEventListener("DOMContentLoaded", function() {
        const targetElement = document.getElementById("typewriter");

        function typeWriter() {
            if (index < aboutText.length) {
                targetElement.textContent += aboutText.charAt(index);
                index++;
                setTimeout(typeWriter, speed);
            }
        }
        
        // Triggers the initial delay before calling the typewriter function
        setTimeout(typeWriter, initialDelay);
    });
</script>
