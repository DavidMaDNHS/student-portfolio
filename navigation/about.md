---
layout: post
title: About
description: My Name is David! Here is my story and Portfolio!
permalink: /about/
comments: true
---

## My Story
Hi! I am David Ma! Welcome to my ABOUT PAGE!

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

<!-- 🦐 Favorite Food 🍪 -->
<h2 style="text-align:center; margin-top: 10px;">🦐 Favorite Food 🍪</h2>

<div style="display:flex; justify-content:center; gap:15px; flex-wrap:nowrap; margin-bottom:20px; align-items:center;">
  <img src="{{ '/images/about/Acookie.jpg' | relative_url }}" alt="Cookie" style="width:150px; border-radius:8px;">
  <img src="{{ '/images/about/Asushi.jpg' | relative_url }}" alt="Sushi" style="width:300px; border-radius:16px;">
  <img src="{{ '/images/about/Ajjamppong.jpg' | relative_url }}" alt="Jjamppong" style="width:150px; border-radius:8px;">
</div>

### Favorite Food

- 🍜🌶️🦀Jjamppong(Korean Spicy Seafood Noodles)
- 🍲Italian style Zuppa Toscana Soup
- 🍪Chocolate Chip Cookies
- 🍣Sushi
- 🍛Japanese Curry
- 🍗Kentucky Fried Chicken

---

<!-- 🎨 ACCOMPLISHMENTS -->
<h2 style="text-align:center; margin-top: 10px;">Accomplishments</h2>

<div style="display:flex; justify-content:center; gap:15px; flex-wrap:wrap; margin-bottom:20px; align-items:flex-start;">
  <img src="{{ '/images/about/Artaccomplishment1.jpg' | relative_url }}" alt="Art Accomplishment 1" style="width:auto; max-width:300px; border-radius:8px;">
  <img src="{{ '/images/about/Artaccomplishment2.jpg' | relative_url }}" alt="Art Accomplishment 2" style="width:auto; max-width:300px; border-radius:8px;">
</div>

### Achievements 🏆

Throughout my journey, I’ve worked hard to grow in both academics and hobbies, and I’m proud of a few milestones:

- 🎨 **Art Competitions** — Won multiple San Diego–area art contests, showcasing my creativity and unique style.  
- ♟️ **Chess Tournaments** — Competed and placed in several local tournaments, building strategy and focus.  
- 🌟 **Personal Growth** — Learned to adapt to a new country and culture, while discovering passions that continue to inspire me every day.  

---

### Nature
I also love the Nature and its wonderful landscapes!

<!-- 🌿 Nature Photo -->
<div style="text-align:center; margin:30px 0;">
  <img src="{{ '/images/about/ANature.jpg' | relative_url }}" alt="Nature Photo">
</div>

### Closing

My journey has been full of change — from Shanghai to San Diego — but I’ve learned to adapt, find new passions, and grow along the way.  

I hope you found my story interesting!
