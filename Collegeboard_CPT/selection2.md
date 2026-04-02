---
layout: post
title: "Training Selection"
description: "Choose one of the modules to add to your training itinerary."
permalink: /chess/selection/
parent: "Chess Hub"
footer: 
    previous: /chess/helper/
    home: /chess/
    next: /chess/trainer/
---
<html lang="en">
<head>
    <style>
        body {
            font-family: 'Georgia', serif;
            background: #1e391a;
            color: white;
            margin: 0; padding: 0;
            display: flex; justify-content: center;
        }

        .container { 
            max-width: 1100px; width: 90%;
            /* Pulled way up to 100px to ensure it's visible immediately */
            margin: 100px auto 40px auto; 
            text-align: center;
        }

        /* --- UPPER LEFT CONTROLS --- */
        .controls-top-left {
            position: fixed;
            top: 70px; 
            left: 20px;
            z-index: 5000;
            display: flex;
            flex-direction: row;
            align-items: flex-start;
            gap: 20px;
        }

        #profileToggle {
            width: 100px; height: 100px;
            background: #ffd700; border: 4px solid #fff;
            border-radius: 50%; cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
            display: flex; align-items: center; justify-content: center;
            overflow: hidden; padding: 0;
        }

        #profileToggle img { width: 100%; height: 100%; object-fit: cover; }

        .clear-logout-btn {
            background: #c0392b; color: white; border: 3px solid #fff;
            padding: 20px; width: 150px; border-radius: 12px;
            font-weight: bold; cursor: pointer; text-transform: uppercase;
            font-size: 1rem; box-shadow: 0 6px 20px rgba(0,0,0,0.4);
            margin-top: 10px;
        }

        #profileMenu {
            display: none; position: absolute;
            top: 110px; left: 0; width: 280px;
            background: rgba(0, 0, 0, 0.95); border: 2px solid #ffd700;
            border-radius: 15px; padding: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.8);
        }

        .profile-header { text-align: center; margin-bottom: 15px; }
        .profile-header img { 
            width: 120px; height: 120px; border-radius: 15px; 
            border: 2px solid #ffd700; object-fit: cover; 
        }

        .prof-input-group { margin-bottom: 10px; text-align: left; }
        .prof-input-group label { font-size: 0.7rem; color: #ffd700; text-transform: uppercase; display: block; margin-bottom: 4px; }
        .prof-input-group input { 
            width: 100%; padding: 8px; background: #222; border: 1px solid #444; 
            color: white; border-radius: 5px;
        }

        .prof-btn { width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px; border: none; cursor: pointer; font-weight: bold; }

        /* --- ITINERARY SIDEBAR --- */
        .itinerary-tracker {
            position: fixed; right: 20px; top: 50%; transform: translateY(-50%);
            width: 280px; background: rgba(0, 0, 0, 0.95); border: 2px solid #ffd700;
            border-radius: 15px; padding: 20px; z-index: 9999;
        }

        .itinerary-item {
            background: rgba(255, 255, 255, 0.1); border-radius: 8px; padding: 10px; 
            margin-bottom: 8px; border-left: 4px solid #ffd700; text-align: left;
        }

        .diff-btn {
            background: #2c3e50; color: white; border: 1px solid #ffd700;
            padding: 8px 12px; margin: 4px; font-size: 0.75rem; border-radius: 5px; 
            cursor: pointer; font-weight: bold; transition: 0.2s;
        }

        /* --- CENTERED LESSON GRID --- */
        .places-grid { 
            display: flex; flex-wrap: wrap; justify-content: center; align-items: center;
            gap: 30px; margin: 20px auto; width: 100%;
        }

        .place-card { 
            background: #1a1a1a; border: 2px solid #ffd700; 
            border-radius: 12px; padding: 25px; width: 280px; 
        }

        .btn { background: #ffd700; color: #1a2332; padding: 12px 25px; border-radius: 25px; cursor: pointer; font-weight: bold; border: none; }
    </style>
</head>
<body>

    <div class="controls-top-left">
        <div style="position: relative;">
            <button id="profileToggle" onclick="toggleProfile()">
                <img id="navAvatar" src="" style="display:none;">
                <span id="profilePlaceholder">👤</span>
            </button>
            <div id="profileMenu">
                <div class="profile-header">
                    <img id="displayAvatar" src="https://via.placeholder.com/120" alt="Avatar">
                    <input type="file" id="avatarUpload" style="display:none" onchange="previewAvatar(event)">
                    <button class="prof-btn" style="background:#444; color:#fff;" onclick="document.getElementById('avatarUpload').click()">Change Photo</button>
                </div>
                <div class="prof-input-group"><label>Username</label><input type="text" id="editUser"></div>
                <div class="prof-input-group"><label>Email</label><input type="email" id="editEmail"></div>
                <div class="prof-input-group"><label>New Password</label><input type="password" id="editPass" placeholder="Leave blank to keep current"></div>
                <button class="prof-btn" style="background:#ffd700; color:#000;" onclick="saveProfile()">Save Changes</button>
            </div>
        </div>
        <button class="clear-logout-btn" onclick="logout()">Logout</button>
    </div>

    <div class="itinerary-tracker">
        <h3 style="color:#ffd700; text-align:center; margin-top:0;">Live Plan</h3>
        <div style="margin-bottom: 20px; text-align: center; border-bottom: 1px solid #444; padding-bottom: 10px;">
            <div style="font-size: 0.7rem; color: #ffd700; font-weight: bold; margin-bottom: 5px;">SWITCH LEVEL</div>
            <button class="diff-btn" onclick="updateLevel('Beginner')">BEG</button>
            <button class="diff-btn" onclick="updateLevel('Intermediate')">INT</button>
            <button class="diff-btn" onclick="updateLevel('Advanced')">ADV</button>
        </div>
        <div class="itinerary-item">
            <div style="font-size: 0.7rem; color: #ffd700; font-weight: bold;">STUDENT</div>
            <div id="sideUser" style="color: #fff;">Guest</div>
        </div>
        <div class="itinerary-item">
            <div style="font-size: 0.7rem; color: #ffd700; font-weight: bold;">SKILL</div>
            <div id="sideLevel" style="color: #fff;">Not set</div>
        </div>
    </div>

    <div class="container">
        <h2 id="welcomeMsg" style="color: #fff; margin-bottom: 5px;">Welcome!</h2>
        <h1 id="dynamicHeading" style="color: #ffd700; font-size: 2.5rem; margin-top: 0;">Chess Plan</h1>
        <div id="places-grid" class="places-grid"></div>
    </div>

    <script>
        const chessLessons = [
            { name: "Piece Movement", type: "Beginner", desc: "Master how the 6 pieces capture.", icon: "🐣" },
            { name: "Board Anatomy", type: "Beginner", desc: "Files, ranks, and center control.", icon: "🗺️" },
            { name: "First Checkmate", type: "Beginner", desc: "The ladder mate and basic wins.", icon: "🍼" },
            { name: "Scholar's Mate", type: "Intermediate", desc: "The classic 4-move attack.", icon: "🪤" },
            { name: "Tactical Forks", type: "Intermediate", desc: "Winning two pieces at once.", icon: "🍴" },
            { name: "Castling Rules", type: "Intermediate", desc: "Keeping your King safe early.", icon: "🏰" },
            { name: "Positional Play", type: "Advanced", desc: "Outposts and weak squares.", icon: "🧠" },
            { name: "Endgame Grinds", type: "Advanced", desc: "Lucena and Philidor positions.", icon: "⏳" },
            { name: "Sicilian Defense", type: "Advanced", desc: "Deep theory for black.", icon: "📖" }
        ];

        function updateLevel(newLvl) {
            let data = JSON.parse(localStorage.getItem('chessItinerary')) || {};
            data.level = newLvl;
            localStorage.setItem('chessItinerary', JSON.stringify(data));
            location.reload(); 
        }

        function toggleProfile() {
            const menu = document.getElementById('profileMenu');
            menu.style.display = (menu.style.display === 'block') ? 'none' : 'block';
        }

        function previewAvatar(event) {
            const reader = new FileReader();
            reader.onload = function() { document.getElementById('displayAvatar').src = reader.result; }
            reader.readAsDataURL(event.target.files[0]);
        }

        function saveProfile() {
            const session = localStorage.getItem("chess_academy_session");
            let users = JSON.parse(localStorage.getItem("chess_academy_users")) || [];
            const idx = users.findIndex(u => u.username === session);
            if(idx !== -1) {
                users[idx].username = document.getElementById('editUser').value;
                users[idx].email = document.getElementById('editEmail').value;
                users[idx].photo = document.getElementById('displayAvatar').src;
                const newPass = document.getElementById('editPass').value;
                if(newPass) users[idx].password = newPass;
                localStorage.setItem("chess_academy_users", JSON.stringify(users));
                localStorage.setItem("chess_academy_session", users[idx].username);
                location.reload();
            }
        }

        function logout() {
            localStorage.removeItem("chess_academy_session");
            window.location.href = "{{ site.baseurl }}/chess/helper/";
        }

        window.onload = function() {
            const session = localStorage.getItem("chess_academy_session");
            const users = JSON.parse(localStorage.getItem("chess_academy_users")) || [];
            const user = users.find(u => u.username === session);
            if (!user) { window.location.href = "{{ site.baseurl }}/chess/helper/"; return; }

            document.getElementById('welcomeMsg').innerText = "Welcome, " + user.username + "!";
            document.getElementById('sideUser').innerText = user.username;
            document.getElementById('editUser').value = user.username;
            document.getElementById('editEmail').value = user.email || "";
            
            const userPhoto = user.photo || "";
            if(userPhoto) {
                document.getElementById('displayAvatar').src = userPhoto;
                document.getElementById('navAvatar').src = userPhoto;
                document.getElementById('navAvatar').style.display = "block";
                document.getElementById('profilePlaceholder').style.display = "none";
            }

            const data = JSON.parse(localStorage.getItem('chessItinerary')) || { level: 'Beginner' };
            document.getElementById('sideLevel').innerText = data.level;
            document.getElementById('dynamicHeading').innerText = data.level + " Chess Plan";

            const grid = document.getElementById('places-grid');
            chessLessons.filter(l => l.type === data.level).forEach(lesson => {
                const card = document.createElement('div');
                card.className = 'place-card';
                card.innerHTML = `
                    <div style="font-size: 3em;">${lesson.icon}</div>
                    <h3>${lesson.name}</h3>
                    <p>${lesson.desc}</p>
                    <button class="btn" onclick="saveSelection('${lesson.name}')">Start Module</button>
                `;
                grid.appendChild(card);
            });
        };

        function saveSelection(name) {
            let data = JSON.parse(localStorage.getItem('chessItinerary')) || {};
            data.selectedModule = name;
            localStorage.setItem('chessItinerary', JSON.stringify(data));
            window.location.href = "{{ site.baseurl }}/chess/trainer/";
        }
    </script>
</body>
</html>