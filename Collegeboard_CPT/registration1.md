---
layout: post
title: "Chess Academy Login"
description: "A tool to find the perfect chess lessons."
permalink: /chess/helper/
parent: "Chess"
submodule: 1
footer:
  previous: /chess/
  home: /chess/
  next: /chess/selection/
---

<html lang="en">
<head>
    <style>
        /* 1. Reset & Layout */
        * { margin: 0; padding: 0; box-sizing: border-box; border: none; }
        body { 
            font-family: 'Georgia', serif; 
            background: #1e391a; 
            color: white; 
            min-height: 100vh;
            overflow: hidden; 
            display: flex;
            position: relative;
        }

        /* RIGHT-SIDE CONTACT PANEL (300px) */
        #contactSidebar { 
            position: fixed; right: -320px; top: 0; width: 300px; height: 100%; 
            background: rgba(0, 0, 0, 0.98); border-left: 2px solid #ffd700; 
            transition: 0.4s; z-index: 9999; padding: 30px; display: flex; flex-direction: column; 
        }
        #contactSidebar.active { right: 0; }
        
        .close-contact { 
            background: #4682B4 !important; color: white !important; padding: 16px; 
            text-align: center; cursor: pointer; font-weight: bold; border-radius: 8px; 
            margin-top: 20px; margin-bottom: 30px; border: 1px solid rgba(255,255,255,0.3); text-transform: uppercase; 
        }
        .contact-toggle { 
            position: fixed; right: 0; top: 50%; transform: translateY(-50%); 
            background: #ffd700; color: #1e391a; padding: 20px 12px; cursor: pointer; 
            border-radius: 10px 0 0 10px; font-weight: bold; z-index: 1500; 
            writing-mode: vertical-rl; text-orientation: mixed; 
        }

        /* LEFT-SIDE NAVIGATION (300px) */
        .sidebar {
            width: 300px; background: rgba(0, 0, 0, 0.95); padding: 40px 25px;
            display: flex; flex-direction: column; position: fixed; left: 0; top: 0; height: 100vh; z-index: 100;
        }
        .sidebar h2 { color: #ffd700; font-size: 1.6rem; margin-bottom: 35px; text-align: center; border-bottom: 2px solid #ffd700; padding-bottom: 15px; }
        .category-item {
            padding: 18px; margin: 10px 0; color: #ffffff !important; text-decoration: none; 
            background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 215, 0, 0.3) !important; 
            border-radius: 6px; transition: 0.3s; font-weight: bold; display: block; text-align: center;
        }
        .category-item:hover { background: #ffd700; color: #1e391a !important; }

        /* DEAD CENTER CONTAINER */
        .container { 
            background: rgba(0,0,0,0.85); padding: 60px; border-radius: 15px; border: 2px solid #ffd700; 
            width: 100%; max-width: 550px; box-shadow: 0 15px 60px rgba(0,0,0,0.9);
            position: fixed; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 50;
        }
        h2, h3 { color: #ffd700; text-align: center; margin-bottom: 30px; font-size: 2.2rem; }
        label { display: block; margin-top: 20px; color: #ffd700; font-weight: bold; text-align: center; font-size: 1.2rem; }

        input, select { 
            width: 100%; padding: 18px; margin: 15px 0; border-radius: 10px; 
            background: #222; color: white; border: 1px solid #444; font-size: 1.1rem;
        }

        /* WARM YELLOW BUTTONS */
        .btn { 
            background: #ffcc00; color: #1e391a; padding: 20px; width: 100%; 
            border: none; font-weight: bold; cursor: pointer; border-radius: 50px; 
            margin-top: 25px; transition: 0.3s; font-size: 1.2rem; text-transform: uppercase;
        }
        .btn:hover { transform: scale(1.05); background: #fff; }

        .back-link { display: block; text-align: center; margin-top: 25px; color: #ffd700; cursor: pointer; text-decoration: underline; font-size: 1rem; }
        .status-msg { text-align: center; margin-top: 20px; font-weight: bold; color: #ffd700; }
        .hidden { display: none; }
    </style>
</head>
<body>

    <div class="contact-toggle" onclick="toggleContact()">CONTACT US</div>
    <div id="contactSidebar">
        <div class="close-contact" onclick="toggleContact()">✕ COLLAPSE PANEL</div>
        <h2 style="font-size: 1.4rem; text-align: center; color: #ffd700; margin-bottom: 20px;">Support Hub</h2>
        <form action="https://formspree.io/f/YOUR_ID" method="POST">
            <input type="email" name="email" placeholder="Your Email" required style="width: 100%; padding: 15px; background: #222; color: white; border-radius: 8px; margin-bottom: 15px;">
            <textarea name="message" placeholder="Your Message" required style="height: 120px; width:100%; background:#222; color:white; padding:15px; border-radius:8px; margin-bottom:15px; border:1px solid #444;"></textarea>
            <button type="submit" style="width:100%; padding:18px; background:#ffcc00; color:#1e391a; font-weight:bold; cursor:pointer; border-radius:8px; text-transform: uppercase;">Send Transmission</button>
        </form>
    </div>

    <div class="sidebar">
        <h2>Chess Academy</h2>
        <a href="{{ site.baseurl }}/chess/HTMP/" class="category-item">♟ How to move pieces</a>
        <a href="{{ site.baseurl }}/chess/opening/" class="category-item">🚀 Opening</a>
        <a href="{{ site.baseurl }}/chess/midgame/" class="category-item">⚔️ Midgame</a>
        <a href="{{ site.baseurl }}/chess/endgame/" class="category-item">🏁 Endgame</a>
        <a href="{{ site.baseurl }}/chess/TS/" class="category-item">🧠 Tactics & Strategies</a>
        <a href="{{ site.baseurl }}/chess/overview/" class="category-item">📖 Tool Overview</a>
    </div>

    <div class="container" id="choiceBox">
        <h2>Welcome</h2>
        <button class="btn" onclick="showBox('regBox')">New Registration</button>
        <button class="btn" onclick="showBox('loginBox')">Member Login</button>
    </div>

    <div class="container hidden" id="regBox">
        <h2>Create Account</h2>
        <input type="text" id="regUser" placeholder="New Username">
        <input type="password" id="regPass" placeholder="New Password">
        <button class="btn" onclick="simulateRegistration()">Register</button>
        <span class="back-link" onclick="showBox('choiceBox')">← Back</span>
        <div id="regStatus" class="status-msg"></div>
    </div>

    <div class="container hidden" id="loginBox">
        <h2>Member Login</h2>
        <input type="text" id="loginUser" placeholder="Username">
        <input type="password" id="loginPass" placeholder="Password">
        <button class="btn" onclick="checkLogin()">Login</button>
        <span class="back-link" onclick="showBox('choiceBox')">← Back</span>
    </div>

    <div class="container hidden" id="quizBox">
        <h3>Training Profile</h3>
        <label>What is your skill level?</label>
        <select id="skillLevel">
            <option value="">Select Level...</option>
            <option value="400">Beginner (Under 400)</option>
            <option value="800">Intermediate (400 - 800)</option>
            <option value="1500">Advanced (800 - 1500)</option>
            <option value="Expert">Expert (1500+)</option>
        </select>
        <button class="btn" onclick="saveAndProceed()">Finalize & Start</button>
    </div>

    <script>
        function toggleContact() { document.getElementById('contactSidebar').classList.toggle('active'); }
        function showBox(id) {
            document.querySelectorAll('.container').forEach(c => c.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
        }

        let registeredUser = "admin"; 
        let registeredPass = "1234";

        function simulateRegistration() {
            const user = document.getElementById('regUser').value;
            const pass = document.getElementById('regPass').value;
            if (user.length < 3) { alert("Invalid Username"); return; }
            document.getElementById('regStatus').innerText = "Registering...";
            setTimeout(() => {
                registeredUser = user; registeredPass = pass;
                document.getElementById('regStatus').innerText = "Success! Please Login.";
                setTimeout(() => showBox('loginBox'), 1000);
            }, 800);
        }

        function checkLogin() {
            const user = document.getElementById('loginUser').value;
            const pass = document.getElementById('loginPass').value;
            if (user === registeredUser && pass === registeredPass) {
                showBox('quizBox');
            } else { alert("Incorrect Credentials"); }
        }

        function saveAndProceed() {
            const skill = document.getElementById('skillLevel').value;
            if(!skill) { alert("Please select a level!"); return; }
            localStorage.setItem('chessItinerary', JSON.stringify({ level: skill, user: registeredUser }));
            window.location.href = "{{ site.baseurl }}/chess/selection/";
        }
    </script>
</body>
</html>