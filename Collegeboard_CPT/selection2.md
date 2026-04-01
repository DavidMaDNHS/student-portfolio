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
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
        }

        .container { 
            max-width: 900px; 
            width: 100%;
            margin: 40px 300px 40px 100px; 
            text-align: center;
        }

        /* --- PROFILE BUTTON & MENU (LEFT) --- */
        .profile-wrapper {
            position: fixed;
            left: 20px;
            bottom: 20px;
            z-index: 2000;
        }

        #profileToggle {
            width: 60px;
            height: 60px;
            background: #ffd700;
            border: 2px solid #fff;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            transition: 0.3s;
        }

        #profileMenu {
            display: none;
            position: absolute;
            bottom: 70px;
            left: 0;
            width: 280px;
            background: rgba(0, 0, 0, 0.95);
            border: 2px solid #ffd700;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.8);
        }

        .profile-header { text-align: center; margin-bottom: 15px; }
        .profile-header img { 
            width: 80px; height: 80px; border-radius: 50%; 
            border: 2px solid #ffd700; object-fit: cover; 
        }

        .prof-input-group { margin-bottom: 10px; text-align: left; }
        .prof-input-group label { font-size: 0.7rem; color: #ffd700; text-transform: uppercase; display: block; margin-bottom: 4px; }
        .prof-input-group input { 
            width: 100%; padding: 8px; background: #222; border: 1px solid #444; 
            color: white; border-radius: 5px; font-size: 0.8rem;
        }

        .prof-btn {
            width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px;
            border: none; cursor: pointer; font-weight: bold; font-size: 0.75rem;
        }
        .save-prof { background: #ffd700; color: #000; }
        .logout-prof { background: #c0392b; color: #fff; }

        /* --- THE ITINERARY SIDEBAR (RIGHT) --- */
        .itinerary-tracker {
            position: fixed;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            width: 280px;
            background: rgba(0, 0, 0, 0.9);
            border: 2px solid #ffd700;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            z-index: 1000;
        }

        .itinerary-item {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px; padding: 10px; margin-bottom: 8px;
            border-left: 4px solid #ffd700; text-align: left;
        }

        .itinerary-label { font-size: 0.7rem; color: #ffd700; text-transform: uppercase; font-weight: bold; }
        .itinerary-value { color: #fff; font-size: 0.9rem; }

        .diff-btn {
            background: #2c3e50; color: white; border: 1px solid #ffd700;
            padding: 5px 10px; margin: 2px; font-size: 0.7rem; border-radius: 5px; cursor: pointer;
        }
        .diff-btn:hover { background: #ffd700; color: black; }

        .places-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .place-card {
            background: #1a1a1a; border-radius: 12px; padding: 25px;
            border: 2px solid #ffd700; transition: 0.3s;
        }
        .place-card:hover { transform: translateY(-5px); box-shadow: 0 0 20px gold; }

        .btn {
            background: #ffd700; color: #1a2332; border: none; padding: 12px 25px;
            border-radius: 25px; cursor: pointer; font-weight: bold; margin-top: 15px;
        }
    </style>
</head>
<body>

    <div class="profile-wrapper">
        <div id="profileMenu">
            <div class="profile-header">
                <img id="displayAvatar" src="https://via.placeholder.com/80" alt="Avatar">
                <input type="file" id="avatarUpload" style="display:none" onchange="previewAvatar(event)">
                <button class="prof-btn" style="background:#444; color:#fff;" onclick="document.getElementById('avatarUpload').click()">Change Photo</button>
            </div>
            
            <div class="prof-input-group">
                <label>Username</label>
                <input type="text" id="editUser">
            </div>
            <div class="prof-input-group">
                <label>Email</label>
                <input type="email" id="editEmail">
            </div>
            <div class="prof-input-group">
                <label>New Password</label>
                <input type="password" id="editPass" placeholder="Leave blank to keep current">
            </div>

            <button class="prof-btn save-prof" onclick="saveProfile()">Save Changes</button>
            <button class="prof-btn logout-prof" onclick="logout()">Log Out</button>
        </div>
        <button id="profileToggle" onclick="toggleProfile()">👤</button>
    </div>

    <div class="itinerary-tracker">
        <h3 style="color:#ffd700; text-align:center; margin-top:0;">Live Plan</h3>
        <div style="margin-bottom: 15px; text-align: center;">
            <div class="itinerary-label" style="margin-bottom:5px;">Change Level</div>
            <button class="diff-btn" onclick="updateLevel('Beginner')">BEG</button>
            <button class="diff-btn" onclick="updateLevel('Intermediate')">INT</button>
            <button class="diff-btn" onclick="updateLevel('Advanced')">ADV</button>
        </div>

        <div class="itinerary-item">
            <div class="itinerary-label">Student</div>
            <div id="sideUser" class="itinerary-value">Guest</div>
        </div>
        <div class="itinerary-item">
            <div class="itinerary-label">Current Skill</div>
            <div id="sideLevel" class="itinerary-value">Not set</div>
        </div>
        <div id="itineraryList"></div>
    </div>

    <div class="container">
        <h1 style="color: #ffd700; font-size: 2.5rem;">♟️ Training Selection</h1>
        <p>Your Advisor has filtered the database for <strong><span id="displayLevel"></span></strong> modules.</p>
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

        /* PROFILE FUNCTIONS */
        function toggleProfile() {
            const menu = document.getElementById('profileMenu');
            menu.style.display = (menu.style.display === 'block') ? 'none' : 'block';
        }

        function previewAvatar(event) {
            const reader = new FileReader();
            reader.onload = function() {
                document.getElementById('displayAvatar').src = reader.result;
            }
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
                alert("Profile Updated!");
                location.reload();
            }
        }

        function logout() {
            localStorage.removeItem("chess_academy_session");
            window.location.href = "{{ site.baseurl }}/chess/helper/";
        }

        /* CORE LESSON FUNCTIONS */
        function updateLevel(newLvl) {
            let data = JSON.parse(localStorage.getItem('chessItinerary'));
            if(data) {
                data.level = newLvl;
                localStorage.setItem('chessItinerary', JSON.stringify(data));
                location.reload(); 
            }
        }

        function loadSelection() {
            const session = localStorage.getItem("chess_academy_session");
            const users = JSON.parse(localStorage.getItem("chess_academy_users")) || [];
            const user = users.find(u => u.username === session);

            if (!user) {
                window.location.href = "{{ site.baseurl }}/chess/helper/";
                return;
            }

            // Populate Profile Editor
            document.getElementById('editUser').value = user.username;
            document.getElementById('editEmail').value = user.email || "";
            document.getElementById('displayAvatar').src = user.photo || "https://via.placeholder.com/80";

            const data = JSON.parse(localStorage.getItem('chessItinerary'));
            const progress = JSON.parse(localStorage.getItem('chessProgress')) || { completedCount: 0 };
            
            if (!data) return;

            document.getElementById('sideUser').innerText = user.username;
            document.getElementById('sideLevel').innerText = data.level;
            document.getElementById('displayLevel').innerText = data.level;

            const listContainer = document.getElementById('itineraryList');
            if (data.lessons) {
                listContainer.innerHTML = '<div class="itinerary-label" style="margin: 10px 0 5px 5px;">Your Roadmap</div>';
                data.lessons.forEach((lessonName, index) => {
                    const isDone = index < progress.completedCount;
                    const item = document.createElement('div');
                    item.className = 'itinerary-item';
                    item.innerHTML = `
                        <div class="itinerary-label">Step ${index + 1} ${isDone ? '✅' : ''}</div>
                        <div class="itinerary-value">${lessonName}</div>
                    `;
                    listContainer.appendChild(item);
                });
            }

            const grid = document.getElementById('places-grid');
            chessLessons.forEach(lesson => {
                if (lesson.type === data.level) {
                    const card = document.createElement('div');
                    card.className = 'place-card';
                    card.innerHTML = `
                        <div style="font-size: 3em; margin-bottom: 10px;">${lesson.icon}</div>
                        <h3>${lesson.name}</h3>
                        <p>${lesson.desc}</p>
                        <button class="btn" onclick="saveSelection('${lesson.name}')">Start Module</button>
                    `;
                    grid.appendChild(card);
                }
            });
        }

        function saveSelection(lessonName) {
            let data = JSON.parse(localStorage.getItem('chessItinerary'));
            data.selectedModule = lessonName;
            localStorage.setItem('chessItinerary', JSON.stringify(data));
            window.location.href = "{{ site.baseurl }}/chess/trainer/";
        }

        window.onload = loadSelection;
    </script>
</body>
</html>