---
layout: single
author_profile: true
title: Categories
header:
  overlay_image: ZenBG.png
permalink: /categories.html
---

<script>
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
    
    
    <div class="type-wrap">
            <div id="typed-strings">
                <span>Typed.js is a <strong>jQuery</strong> plugin.</span>
                <p>It <em>types</em> out sentences.</p>
                <p>And then deletes them.</p>
                <p>Try it out!</p>
            </div>
            <span id="typed" style="white-space:pre;"></span>
        </div>

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
