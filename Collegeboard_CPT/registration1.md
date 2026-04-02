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

        /* RIGHT-SIDE CONTACT PANEL */
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

        /* LEFT-SIDE NAVIGATION */
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

        /* CONTAINER */
        .container { 
            background: rgba(0,0,0,0.85); padding: 50px; border-radius: 15px; border: 2px solid #ffd700; 
            width: 100%; max-width: 500px; box-shadow: 0 15px 60px rgba(0,0,0,0.9);
            position: fixed; left: 50%; top: 50%; transform: translate(-50%, -50%); z-index: 50;
        }
        h2, h3 { color: #ffd700; text-align: center; margin-bottom: 25px; font-size: 2rem; }
        label { display: block; margin-top: 15px; color: #ffd700; font-weight: bold; text-align: center; font-size: 1.1rem; }

        input, select { 
            width: 100%; padding: 15px; margin: 10px 0; border-radius: 8px; 
            background: #222; color: white; border: 1px solid #444; font-size: 1rem;
        }

        .btn { 
            background: #ffcc00; color: #1e391a; padding: 18px; width: 100%; 
            border: none; font-weight: bold; cursor: pointer; border-radius: 50px; 
            margin-top: 20px; transition: 0.3s; font-size: 1.1rem; text-transform: uppercase;
        }
        .btn:hover { transform: scale(1.05); background: #fff; }

        .back-link { display: block; text-align: center; margin-top: 20px; color: #ffd700; cursor: pointer; text-decoration: underline; font-size: 0.9rem; }
        .status-msg { text-align: center; margin-top: 15px; font-weight: bold; color: #ffd700; }
        .hidden { display: none; }
    </style>
</head>
<body>

    <div class="contact-toggle" onclick="toggleContact()">CONTACT US</div>
    <div id="contactSidebar">
        <div class="close-contact" onclick="toggleContact()">✕ COLLAPSE PANEL</div>
        <h2 style="font-size: 1.4rem; text-align: center; color: #ffd700; margin-bottom: 20px;">Support Hub</h2>
        <form action="https://formspree.io/f/YOUR_ID" method="POST">
            <input type="email" name="email" placeholder="Your Email" required>
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
    </div>

    <div class="container" id="choiceBox">
        <h2>Grandmaster Entry</h2>
        <button class="btn" onclick="showBox('regBox')">Create New Account</button>
        <button class="btn" onclick="showBox('loginBox')">Login to Account</button>
    </div>

    <div class="container hidden" id="regBox">
        <h2>New Registration</h2>
        <input type="text" id="regUser" placeholder="Desired Username">
        <input type="email" id="regEmail" placeholder="Email Address">
        <input type="password" id="regPass" placeholder="Secure Password">
        <button class="btn" onclick="handleRegistration()">Register Account</button>
        <span class="back-link" onclick="showBox('choiceBox')">← Back</span>
        <div id="regStatus" class="status-msg"></div>
    </div>

    <div class="container hidden" id="loginBox">
        <h2>Member Login</h2>
        <input type="text" id="loginUser" placeholder="Username">
        <input type="password" id="loginPass" placeholder="Password">
        <button class="btn" onclick="handleLogin()">Sign In</button>
        <span class="back-link" onclick="showBox('choiceBox')">← Back</span>
    </div>

    <div class="container hidden" id="quizBox">
        <h3 id="welcomeHeader">Training Profile</h3>
        <label>Set your training level:</label>
        <select id="skillLevel">
            <option value="">Choose your rank...</option>
            <option value="Beginner">Beginner (Under 400)</option>
            <option value="Intermediate">Intermediate (400 - 1200)</option>
            <option value="Advanced">Advanced (1200 - 2000)</option>
            <option value="Expert">Master (2000+)</option>
        </select>
        <button class="btn" onclick="saveAndProceed()">Launch Training</button>
        <span class="back-link" onclick="logout()">Log Out / Switch Account</span>
    </div>

    <script>
        const STORAGE_KEY = "chess_academy_users";
        const SESSION_KEY = "chess_academy_session";

        function toggleContact() { document.getElementById('contactSidebar').classList.toggle('active'); }
        
        function showBox(id) {
            document.querySelectorAll('.container').forEach(c => c.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
        }

        function getUsers() {
            return JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
        }

        // AUTO-CHECK SESSION: If logged in, skip to Quiz
        window.onload = function() {
            const activeSession = localStorage.getItem(SESSION_KEY);
            if (activeSession) {
                document.getElementById('welcomeHeader').innerText = `Welcome Back, ${activeSession}`;
                showBox('quizBox');
            }
        };

        function handleRegistration() {
            const user = document.getElementById('regUser').value.trim();
            const email = document.getElementById('regEmail').value.trim();
            const pass = document.getElementById('regPass').value.trim();
            const status = document.getElementById('regStatus');

            if (!user || !email || !pass) {
                alert("Please fill all fields.");
                return;
            }

            let users = getUsers();
            if (users.find(u => u.username === user)) {
                alert("Username is taken!");
                return;
            }

            status.innerText = "Securing account...";
            
            setTimeout(() => {
                // Store user object with email for the profile page
                users.push({ username: user, email: email, password: pass, photo: "" });
                localStorage.setItem(STORAGE_KEY, JSON.stringify(users));
                status.innerText = "Account Created! Redirecting to Login...";
                setTimeout(() => showBox('loginBox'), 1000);
            }, 800);
        }

        function handleLogin() {
            const user = document.getElementById('loginUser').value.trim();
            const pass = document.getElementById('loginPass').value.trim();
            const users = getUsers();

            const foundUser = users.find(u => u.username === user && u.password === pass);

            if (foundUser) {
                localStorage.setItem(SESSION_KEY, user); // SET PERMANENT SESSION
                document.getElementById('welcomeHeader').innerText = `Welcome, ${user}`;
                showBox('quizBox');
            } else {
                alert("Invalid Username or Password.");
            }
        }

        function saveAndProceed() {
            const skill = document.getElementById('skillLevel').value;
            const currentUser = localStorage.getItem(SESSION_KEY);

            if(!skill) { alert("Please select your level!"); return; }
            
            // Save itinerary linked to this session
            localStorage.setItem('chessItinerary', JSON.stringify({ 
                level: skill, 
                user: currentUser 
            }));

            window.location.href = "{{ site.baseurl }}/chess/selection/";
        }

        function logout() {
            localStorage.removeItem(SESSION_KEY);
            location.reload();
        }
    </script>
</body>
</html>