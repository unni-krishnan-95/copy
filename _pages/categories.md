---
layout: single
author_profile: true
title: Categories
header:
  overlay_image: ZenBG.png
permalink: /categories.html
---

    $(function(){
        $("#typed").typed({
            // strings: ["Typed.js is a <strong>jQuery</strong> plugin.", "It <em>types</em> out sentences.", "And then deletes them.", "Try it out!"],
            stringsElement: $('#typed-strings'),
            typeSpeed: 30,
            backDelay: 500,
            loop: false,
            contentType: 'html', // or text
            // defaults to false for infinite loop
            loopCount: false,
            callback: function(){ foo(); },
            resetCallback: function() { newTyped(); }
        });
        $(".reset").click(function(){
            $("#typed").typed('reset');
        });
    });
    function newTyped(){ /* A new typed object */ }
    function foo(){ console.log("Callback"); }
    </script>
    <link href="main.css" rel="stylesheet"/>
    <style>
        /* code for animated blinking cursor */
        .typed-cursor{
            opacity: 1;
            font-weight: 100;
            -webkit-animation: blink 0.7s infinite;
            -moz-animation: blink 0.7s infinite;
            -ms-animation: blink 0.7s infinite;
            -o-animation: blink 0.7s infinite;
            animation: blink 0.7s infinite;
        }
        @-keyframes blink{
            0% { opacity:1; }
            50% { opacity:0; }
            100% { opacity:1; }
        }
        @-webkit-keyframes blink{
            0% { opacity:1; }
            50% { opacity:0; }
            100% { opacity:1; }
        }
        @-moz-keyframes blink{
            0% { opacity:1; }
            50% { opacity:0; }
            100% { opacity:1; }
        }
        @-ms-keyframes blink{
            0% { opacity:1; }
            50% { opacity:0; }
            100% { opacity:1; }
        }
        @-o-keyframes blink{
            0% { opacity:1; }
            50% { opacity:0; }
            100% { opacity:1; }
        }
    </style>


A listing of all my posts, sorted by specific Categories - makes it easier to find what you are looking for!

<h2>OverTheWire</h2>
<ul>

<li>Bandit</li>
<ul>
<li><a href="https://jhalon.github.io/over-the-wire-bandit1/">Bandit Solutions 1-10</a></li>
<li><a href="https://jhalon.github.io/over-the-wire-bandit2/">Bandit Solutions 11-25</a></li>
</ul>

<li>Leviathan</li>
<ul>
<li><a href="https://jhalon.github.io/over-the-wire-leviathan/">Leviathan Solutions 1-8</a></li>
</ul>

<li>Natas</li>
<ul>
<li><a href="https://jhalon.github.io/over-the-wire-natas1/">Natas Solutions 1-10</a></li>
<li><a href="https://jhalon.github.io/over-the-wire-natas2/">Natas Solutions 11-15</a></li>
<li><a href="https://jhalon.github.io/over-the-wire-natas3/">Natas Solutions 16-20</a></li>
</ul>

</ul>

<h2>VulnHub</h2>
<ul>
<li>Mr. Robot</li>
</ul>

<h2>General</h2>
<ul>
<li><a href="https://jhalon.github.io/m-trends-fireeye-report-overview/">M-Trends 2016: Cyber Threat Report Overview</a></li>
</ul>
