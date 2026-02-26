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
            margin: 40px 300px 40px 40px; 
            text-align: center;
        }

        /* THE ITINERARY SIDEBAR */
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
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 8px;
            border-left: 4px solid #ffd700;
            text-align: left;
        }

        .itinerary-label { font-size: 0.7rem; color: #ffd700; text-transform: uppercase; font-weight: bold; }
        .itinerary-value { color: #fff; font-size: 0.9rem; }

        /* DIFFICULTY BUTTONS */
        .diff-btn {
            background: #2c3e50;
            color: white;
            border: 1px solid #ffd700;
            padding: 5px 10px;
            margin: 2px;
            font-size: 0.7rem;
            border-radius: 5px;
            cursor: pointer;
        }
        .diff-btn:hover { background: #ffd700; color: black; }

        .places-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .place-card {
            background: #1a1a1a;
            border-radius: 12px;
            padding: 25px;
            border: 2px solid #ffd700;
            transition: 0.3s;
        }
        .place-card:hover { transform: translateY(-5px); box-shadow: 0 0 20px gold; }

        .btn {
            background: #ffd700;
            color: #1a2332;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 15px;
        }
    </style>
</head>
<body>

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

        <div id="itineraryList">
            </div>
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

        function updateLevel(newLvl) {
            let data = JSON.parse(localStorage.getItem('chessItinerary'));
            if(data) {
                data.level = newLvl;
                localStorage.setItem('chessItinerary', JSON.stringify(data));
                location.reload(); 
            }
        }

        function loadSelection() {
            const data = JSON.parse(localStorage.getItem('chessItinerary'));
            const progress = JSON.parse(localStorage.getItem('chessProgress')) || { completedCount: 0 };
            if (!data) return;

            document.getElementById('sideUser').innerText = data.user || "Player";
            document.getElementById('sideLevel').innerText = data.level;
            document.getElementById('displayLevel').innerText = data.level;

            // FIX: Show the 3 random lessons in the sidebar instead of "Selecting..."
            const listContainer = document.getElementById('itineraryList');
            if (data.lessons) {
                listContainer.innerHTML = '<div class="itinerary-label" style="margin: 10px 0 5px 5px;">Your Roadmap</div>';
                data.lessons.forEach((lessonName, index) => {
                    const isDone = index < progress.completedCount;
                    const item = document.createElement('div');
                    item.className = 'itinerary-item';
                    if (index === progress.completedCount) item.style.borderLeft = "4px solid #fff";
                    item.style.opacity = isDone ? "0.5" : "1";
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