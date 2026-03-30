---
layout: post
title: "Chess Helper"
description: "A tool to find the perfect chess lessons."
permalink: /chess/helper/
parent: "Chess Hub"
submodule: 1
footer:
  previous: /chess/
  home: /chess/
  next: /chess/selection/
---

<html lang="en">
<head>
    <style>
        /* FIX: Removed the margin-left: 280px to get rid of the black bar */
        body { 
            font-family: 'Georgia', serif; 
            background: #1e391a; 
            color: white; 
            margin: 0; 
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        
        .container { 
            background: rgba(0,0,0,0.85); 
            padding: 40px; 
            border-radius: 15px; 
            border: 2px solid #ffd700; 
            max-width: 450px; 
            width: 90%;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
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

    <div class="container" id="regBox">
        <h2>New Student Registration</h2>
        <input type="text" id="regUser" placeholder="Create Username">
        <input type="password" id="regPass" placeholder="Create Password">
        <button class="btn" onclick="simulateRegistration()">Register Account</button>
        <div id="regStatus" class="status-msg"></div>
    </div>

    <div class="container hidden" id="loginBox">
        <h2>Member Login</h2>
        <p style="text-align: center; font-size: 0.9rem;">Please login with your new credentials</p>
        <input type="text" id="loginUser" placeholder="Username">
        <input type="password" id="loginPass" placeholder="Password">
        <button class="btn" onclick="checkLogin()">Login to Chess Hub</button>
    </div>

    <div class="container hidden" id="quizBox">
        <h3>♟️ Training Profile</h3>
        <label>Choose Your Skill Level:</label>
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
        let registeredUser = "";
        let registeredPass = "";

        // SIMULATED API CALL
        function simulateRegistration() {
            const user = document.getElementById('regUser').value;
            const pass = document.getElementById('regPass').value;

            if (user.length < 3) {
                alert("Username too short!");
                return;
            }

            document.getElementById('regStatus').innerText = "Connecting to Chess Server...";
            
            // This mimics a real API delay
            setTimeout(() => {
                registeredUser = user;
                registeredPass = pass;
                document.getElementById('regStatus').innerText = "Registration Confirmed!";
                
                // Switch boxes after a short delay
                setTimeout(() => {
                    document.getElementById('regBox').classList.add('hidden');
                    document.getElementById('loginBox').classList.remove('hidden');
                }, 1000);
            }, 1500);
        }

        function checkLogin() {
            const user = document.getElementById('loginUser').value;
            const pass = document.getElementById('loginPass').value;

            if (user === registeredUser && pass === registeredPass) {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('quizBox').classList.remove('hidden');
            } else {
                alert("Invalid Credentials!");
            }
        }

        function saveAndProceed() {
            const skill = document.getElementById('skillLevel').value;
            const piece = document.getElementById('favPiece').value;

            if(!skill || !piece) {
                alert("Please select your level and piece!");
                return;
            }

            const chessItinerary = {
                level: skill,
                style: piece,
                user: registeredUser
            };

            localStorage.setItem('chessItinerary', JSON.stringify(chessItinerary));
            // FIXED LINK: Sends you to Step 2
            window.location.href = "{{ site.baseurl }}/chess/selection/";
        }
    </script>
</body>
</html>