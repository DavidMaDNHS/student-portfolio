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
        /* 1. Reset all default margins/padding to force sidebar to the glass edge */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body { 
            font-family: 'Georgia', serif; 
            background: #1e391a; 
            color: white; 
            display: flex;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* 2. Sidebar - Locked to the absolute left boundary */
        .sidebar {
            width: 300px;
            background: rgba(0, 0, 0, 0.9);
            border-right: 2px solid #ffd700;
            padding: 30px 20px;
            display: flex;
            flex-direction: column;
            position: fixed; /* Fixes it to the viewport */
            left: 0;         /* Absolute left */
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
            margin: 5px 0;
            color: #eee;
            text-decoration: none; 
            border-radius: 8px;
            transition: 0.3s;
            font-weight: bold;
            display: block;
        }

        .category-item:hover {
            background: rgba(255, 215, 0, 0.2);
            color: #ffd700;
        }

        /* 3. Main Content - Flex centering logic */
        .main-content {
            margin-left: 300px; /* Offset by sidebar width */
            flex: 1;            /* Take up all remaining space */
            display: flex;
            justify-content: center; /* Horizontal center */
            align-items: center;     /* Vertical center */
            min-height: 100vh;
            padding: 40px;
        }

        .container { 
            background: rgba(0,0,0,0.85); 
            padding: 40px; 
            border-radius: 15px; 
            border: 2px solid #ffd700; 
            width: 100%;
            max-width: 400px; 
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            /* Ensures box doesn't move if content inside changes slightly */
            flex-shrink: 0; 
        }

        h2, h3 { color: #ffd700; text-align: center; margin-bottom: 20px; }
        
        input, select { 
            width: 100%; padding: 12px; margin: 10px 0; 
            border-radius: 8px; background: #222; color: white; 
            border: 1px solid #444; font-size: 1rem;
        }

        .btn { 
            background: #ffd700; color: #1e391a; padding: 15px; 
            width: 100%; border: none; font-weight: bold; 
            cursor: pointer; border-radius: 50px; margin-top: 15px;
            transition: 0.3s;
        }
        .btn:hover { transform: scale(1.02); background: #fff; }

        .status-msg { 
            text-align: center; margin-top: 10px; font-weight: bold; color: #ffd700; 
        }
        .hidden { display: none; }
    </style>
</head>
<body>

    <div class="sidebar">
        <h2>Chess Academy</h2>
        <a href="{{ site.baseurl }}/chess/HTMP/" class="category-item">♟ How to move pieces</a>
        <a href="{{ site.baseurl }}/chess/opening/" class="category-item">🚀 Opening</a>
        <a href="{{ site.baseurl }}/chess/midgame/" class="category-item">⚔️ Midgame</a>
        <a href="{{ site.baseurl }}/chess/endgame/" class="category-item">🏁 Endgame</a>
        <a href="{{ site.baseurl }}/chess/TS/" class="category-item">🧠 Tactics & Strategies</a>
        <a href="{{ site.baseurl }}/chess/overview/" class="category-item">📖 Tool Overview</a>
    </div>

    <div class="main-content">
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
    </div>

    <script>
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