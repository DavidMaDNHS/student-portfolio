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
        /* 1. Reset */
        * { margin: 0; padding: 0; box-sizing: border-box; border: none; }

        body { 
            font-family: 'Georgia', serif; 
            background: #1e391a; 
            color: white; 
            min-height: 100vh;
            overflow: hidden; /* Prevents weird scrollbars */
            display: flex;
        }

        /* RIGHT-SIDE CONTACT PANEL */
        #contactSidebar { 
            position: fixed; 
            right: -320px; 
            top: 0; 
            width: 300px; 
            height: 100%; 
            background: rgba(0, 0, 0, 0.98); 
            border-left: 2px solid #ffd700; 
            transition: 0.4s; 
            z-index: 9999; 
            padding: 25px; 
            display: flex; 
            flex-direction: column; 
        }
        #contactSidebar.active { right: 0; }
        
        .close-contact { 
            background: #4682B4 !important; 
            color: white !important; 
            padding: 14px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: bold; 
            border-radius: 8px; 
            margin-top: 20px; 
            margin-bottom: 30px; 
            border: 1px solid rgba(255,255,255,0.3); 
            text-transform: uppercase; 
        }

        .contact-toggle { 
            position: fixed; 
            right: 0; 
            top: 50%; 
            transform: translateY(-50%); 
            background: #ffd700; 
            color: #1e391a; 
            padding: 15px 10px; 
            cursor: pointer; 
            border-radius: 10px 0 0 10px; 
            font-weight: bold; 
            z-index: 1500; 
            writing-mode: vertical-rl; 
            text-orientation: mixed; 
        }

        /* 2. Left-Side Navigation Sidebar */
        .sidebar {
            width: 300px;
            background: rgba(0, 0, 0, 0.95);
            padding: 30px 20px;
            display: flex;
            flex-direction: column;
            position: fixed;
            left: 0;
            top: 0;
            height: 100vh;
            z-index: 100;
        }

        .sidebar h2 {
            color: #ffd700;
            font-size: 1.5rem;
            margin-bottom: 30px;
            text-align: center;
            border-bottom: 1px solid #ffd700;
            padding-bottom: 10px;
        }

        .category-item {
            padding: 15px;
            margin: 8px 0;
            color: #ffffff !important;
            text-decoration: none; 
            background: rgba(255, 255, 255, 0.05); 
            border: 1px solid rgba(255, 215, 0, 0.3) !important; 
            border-radius: 4px;
            transition: 0.3s;
            font-weight: bold;
            display: block;
            text-align: center;
        }
        .category-item:hover { background: #ffd700; color: #1e391a !important; }

        /* 3. ABSOLUTE SCREEN CENTER FOR THE BOX */
        .container { 
            background: rgba(0,0,0,0.85); 
            padding: 50px; 
            border-radius: 15px; 
            border: 2px solid #ffd700; 
            width: 100%;
            max-width: 500px; 
            box-shadow: 0 10px 50px rgba(0,0,0,0.8);
            
            /* DEAD CENTER LOGIC */
            position: fixed;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            z-index: 50; /* Above background, below slide-out panels */
        }

        h2, h3 { color: #ffd700; text-align: center; margin-bottom: 25px; font-size: 2rem; }
        input, select { 
            width: 100%; padding: 15px; margin: 12px 0; 
            border-radius: 8px; background: #222; color: white; 
            border: 1px solid #444; font-size: 1.1rem;
        }

        .btn { 
            background: #ffd700; color: #1e391a; padding: 18px; 
            width: 100%; border: none; font-weight: bold; 
            cursor: pointer; border-radius: 50px; margin-top: 20px;
            transition: 0.3s; font-size: 1.1rem;
        }
        .btn:hover { transform: scale(1.05); background: #fff; }

        .status-msg { text-align: center; margin-top: 15px; font-weight: bold; color: #ffd700; }
        .hidden { display: none; }

        /* Support Form Styling */
        .contact-form input, .contact-form textarea { 
            width: 100%; padding: 12px; margin-bottom: 15px; background: #222 !important; border: 1px solid #444 !important; color: white !important; border-radius: 5px; 
        }
        .submit-contact { 
            width: 100%; padding: 15px; background: #ffd700; color: #1e391a; border: none; font-weight: bold; cursor: pointer; border-radius: 5px; text-transform: uppercase;
        }
    </style>
</head>
<body>

    <div class="contact-toggle" onclick="toggleContact()">CONTACT US</div>
    <div id="contactSidebar">
        <div class="close-contact" onclick="toggleContact()">✕ COLLAPSE PANEL</div>
        <h2 style="color:#ffd700; text-align:center; margin-bottom:20px; font-size: 1.2rem;">Support Hub</h2>
        <form class="contact-form" action="https://formspree.io/f/YOUR_ID" method="POST">
            <input type="email" name="email" placeholder="Your Email" required>
            <textarea name="message" placeholder="Your Message" required style="height: 100px; width:100%; background:#222; color:white; padding:10px; border-radius:5px; margin-bottom:10px; border:1px solid #444;"></textarea>
            <button type="submit" class="submit-contact">Send Transmission</button>
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

    <div class="container" id="regBox">
        <h2>Student Registration</h2>
        <input type="text" id="regUser" placeholder="Create Username">
        <input type="password" id="regPass" placeholder="Create Password">
        <button class="btn" onclick="simulateRegistration()">Register Account</button>
        <div id="regStatus" class="status-msg"></div>
    </div>

    <div class="container hidden" id="loginBox">
        <h2>Member Login</h2>
        <input type="text" id="loginUser" placeholder="Username">
        <input type="password" id="loginPass" placeholder="Password">
        <button class="btn" onclick="checkLogin()">Login to Chess Hub</button>
    </div>

    <div class="container hidden" id="quizBox">
        <h3>♟️ Training Profile</h3>
        <label>Skill Level:</label>
        <select id="skillLevel">
            <option value="">Select...</option>
            <option value="Beginner">Beginner (0-800)</option>
            <option value="Intermediate">Intermediate (800-1500)</option>
            <option value="Advanced">Advanced (1500+)</option>
        </select>
        <label>Favorite Piece:</label>
        <select id="favPiece">
            <option value="">Select...</option>
            <option value="Knight">Knight</option>
            <option value="Bishop">Bishop</option>
            <option value="Queen">Queen</option>
        </select>
        <button class="btn" onclick="saveAndProceed()">Next: Choose Lessons</button>
    </div>

    <script>
        function toggleContact() { 
            document.getElementById('contactSidebar').classList.toggle('active'); 
        }

        let registeredUser = "";
        let registeredPass = "";

        function simulateRegistration() {
            const user = document.getElementById('regUser').value;
            const pass = document.getElementById('regPass').value;
            if (user.length < 3) { alert("Username too short!"); return; }

            document.getElementById('regStatus').innerText = "Connecting...";
            setTimeout(() => {
                registeredUser = user;
                registeredPass = pass;
                document.getElementById('regStatus').innerText = "Confirmed!";
                setTimeout(() => {
                    document.getElementById('regBox').classList.add('hidden');
                    document.getElementById('loginBox').classList.remove('hidden');
                }, 1000);
            }, 1000);
        }

        function checkLogin() {
            const user = document.getElementById('loginUser').value;
            const pass = document.getElementById('loginPass').value;
            if (user === registeredUser && pass === registeredPass) {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('quizBox').classList.remove('hidden');
            } else { alert("Invalid Credentials!"); }
        }

        function saveAndProceed() {
            const skill = document.getElementById('skillLevel').value;
            const piece = document.getElementById('favPiece').value;
            if(!skill || !piece) { alert("Please select your level and piece!"); return; }
            localStorage.setItem('chessItinerary', JSON.stringify({ level: skill, style: piece, user: registeredUser }));
            window.location.href = "{{ site.baseurl }}/chess/selection/";
        }
    </script>
</body>
</html>