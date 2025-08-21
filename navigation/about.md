---
layout: post
title: About
permalink: /about/
comments: true
---
<!-- ♟️ Falling Chess Pieces -->
<div id="chess-container" aria-hidden="true"></div>

<style>
  #chess-container {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 9999;
    overflow: hidden;
  }

  .chess-piece {
    position: absolute;
    top: -2rem;
    will-change: transform;
    font-size: var(--size, 18px);
    opacity: 0.9;
    user-select: none;
  }

  @keyframes fall {
    0% {
      transform: translate3d(var(--xStart, 0), -5vh, 0) rotate(0deg);
      opacity: 0;
    }
    10% { opacity: 1; }
    100% {
      transform: translate3d(calc(var(--xStart, 0) + var(--xDrift, 0)), 105vh, 0) rotate(360deg);
      opacity: 0.8;
    }
  }
</style>

<script>
(function() {
  const container = document.getElementById('chess-container');
  if (!container) return;

  const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  const PIECES = ['♔','♕','♖','♗','♘','♙']; // White pieces
  const MAX_PIECES = prefersReduced ? 15 : 40; // total on screen at most

  function spawnPiece() {
    if (container.childElementCount >= MAX_PIECES) return;

    const piece = document.createElement('span');
    piece.className = 'chess-piece';
    piece.textContent = PIECES[Math.floor(Math.random() * PIECES.length)];

    // Random size + start position + drift
    const size = Math.floor(Math.random() * 12) + 14; // 14px–26px
    piece.style.setProperty('--size', size + 'px');
    piece.style.setProperty('--xStart', Math.random() * window.innerWidth + 'px');
    piece.style.setProperty('--xDrift', (Math.random() * 100 - 50) + 'px');

    const duration = Math.random() * 8 + 10; // 10–18s
    piece.style.animation = `fall ${duration}s linear forwards`;

    container.appendChild(piece);

    // Remove after animation ends
    setTimeout(() => {
      piece.remove();
    }, duration * 1000);
  }

  // Spawn new pieces periodically
  setInterval(spawnPiece, 1500); // every 1.5s
})();
</script>

## My Story

Here are some of the places I’ve lived.

<style>
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px;
        object-fit: contain;
    }
    .grid-item p {
        margin: 5px 0;
    }
</style>

<div class="grid-container" id="grid_container"></div>

<script>
    var container = document.getElementById("grid_container");
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";

    var living_in_the_world = [
        {"flag": "f/fa/Flag_of_the_People%27s_Republic_of_China.svg", "greeting": "你好", "description": "Shanghai, China — Birth to 2017"},
        {"flag": "a/a4/Flag_of_the_United_States.svg", "greeting": "Hello", "description": "San Diego, California — 2017 to present"},
    ];

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";
        var img = document.createElement("img");
        img.src = http_source + location.flag;
        img.alt = location.flag + " Flag";
        var description = document.createElement("p");
        description.textContent = location.description;
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);
        container.appendChild(gridItem);
    }
</script>

---

### Journey through Life

- 🌏 Born in **Shanghai, China**, lived there until May 25, 2017  
- ✈️ Moved to **San Diego, USA** at age 8  
- 📚 Learned English and adapted to a new culture in about 4 years  
- 🏫 Attended **3 different elementary schools** in San Diego County (moving, bullying, graduation)  
- 🏫 Went to **Oak Valley Middle School**, where I made new friends and grew my hobbies  
- 🏫 Currently a student at **Del Norte High School** (age 16)  

---

### Hobbies and Interests

I’ve developed a lot of hobbies while growing up in both China and the U.S.:

- ♟️ Chess  
- 🎨 Drawing  
- 🦢 Origami  
- 🎮 Playing video games  
- 🥾 Hiking  
- ⚽ Playing soccer  

---

### Achievements 🏆

Throughout my journey, I’ve worked hard to grow in both academics and hobbies, and I’m proud of a few milestones:

- 🎨 **Art Competitions** — Won multiple San Diego–area art contests, showcasing my creativity and unique style.  
- ♟️ **Chess Tournaments** — Competed and placed in several local tournaments, building strategy and focus.  
- 🌟 **Personal Growth** — Learned to adapt to a new country and culture, while discovering passions that continue to inspire me every day.  

---

### Closing

My journey has been full of change — from Shanghai to San Diego — but I’ve learned to adapt, find new passions, and grow along the way.  

I hope you found my story interesting!
