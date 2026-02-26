---
layout: post
title: "Grandmaster Training Room"
permalink: /chess/trainer/
---

<html lang="en">
<head>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background: #1a1a1a; color: white; margin: 0; padding: 20px; }
        
        /* Layout & Header */
        .nav-header { display: flex; justify-content: space-between; align-items: center; padding: 15px 25px; background: #2c3e50; border-radius: 10px; margin-bottom: 25px; border: 1px solid #ffd700; }
        .back-btn { color: #ffd700; cursor: pointer; text-decoration: none; font-weight: bold; font-size: 1rem; }
        .main-layout { display: flex; gap: 30px; flex-wrap: wrap; max-width: 1200px; margin: 0 auto; }

        /* Left Side: Lesson Info */
        .lesson-card { flex: 1; min-width: 350px; background: #262626; padding: 30px; border-radius: 15px; border-top: 5px solid #ffd700; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .lesson-card h2 { color: #ffd700; margin-top: 0; font-size: 2rem; }
        
        .progress-section { margin: 25px 0; }
        .progress-bar { background: #444; height: 18px; border-radius: 10px; overflow: hidden; border: 1px solid #555; margin-top: 8px; }
        #progressFill { background: #2ecc71; width: 0%; height: 100%; transition: 1.2s cubic-bezier(0.175, 0.885, 0.32, 1.275); }

        /* Right Side: Puzzle Board */
        .board-card { flex: 1.2; min-width: 400px; background: #000; padding: 20px; border-radius: 15px; border: 2px solid #ffd700; text-align: center; }
        .board-wrapper { position: relative; width: 100%; padding-bottom: 110%; height: 0; }
        .board-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none; border-radius: 8px; }

        /* Action Button */
        .solve-btn { display: inline-block; margin-top: 25px; padding: 18px 50px; background: #2ecc71; color: white; border: none; border-radius: 50px; font-weight: bold; cursor: pointer; font-size: 1.2rem; transition: 0.3s; box-shadow: 0 4px 15px rgba(46, 204, 113, 0.3); }
        .solve-btn:hover { background: #27ae60; transform: scale(1.05); box-shadow: 0 6px 20px rgba(46, 204, 113, 0.5); }
        
        footer { margin-top: 40px; text-align: center; color: #666; font-size: 0.9rem; border-top: 1px solid #333; padding-top: 20px; }
    </style>
</head>
<body>

    <div class="nav-header">
        <a class="back-btn" onclick="window.location.href='{{ site.baseurl }}/chess/selection/'">← BACK TO SELECTION</a>
        <div style="color: #ffd700; font-weight: bold;">User: <span id="userDisplay"></span></div>
    </div>

    <div class="main-layout">
        <div class="lesson-card">
            <h2 id="moduleTitle">Loading Module...</h2>
            
            <div class="progress-section">
                <span id="progressLabel" style="font-weight: bold; color: #aaa;">Course Progress: 0/3 Lessons</span>
                <div class="progress-bar"><div id="progressFill"></div></div>
            </div>

            <p id="moduleContent" style="line-height: 1.8; font-size: 1.1rem; color: #ddd;"></p>
            
            <div id="advisorTip" style="margin-top: 30px; padding: 20px; background: rgba(255, 215, 0, 0.05); border-radius: 12px; font-style: italic; color: #ffd700; border: 1px dashed #ffd700;">
                </div>
        </div>

        <div class="board-card">
            <h3 style="color: #ffd700; margin-bottom: 15px; letter-spacing: 1px;">PRACTICE ARENA</h3>
            <div class="board-wrapper">
                <iframe id="puzzleFrame" src="" allowtransparency="true"></iframe>
            </div>
            <button class="solve-btn" id="solveBtn" onclick="handleSolve()">I SOLVED IT! 🎉</button>
        </div>
    </div>

    <footer>
        David Ma | Open Coding | Class of 2026
    </footer>

    <script>
        function handleSolve() {
            // 1. Immediate Celebration
            confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 }, colors: ['#ffd700', '#2ecc71', '#ffffff'] });

            // 2. Global Tracking Logic
            let progress = JSON.parse(localStorage.getItem('chessProgress')) || { completedCount: 0 };
            progress.completedCount += 1; // Add 1 point for this lesson
            localStorage.setItem('chessProgress', JSON.stringify(progress));

            // 3. UI Update
            updateUI(progress.completedCount);

            // 4. Crisis-Proof Redirect
            if (progress.completedCount >= 3) {
                // Graduation Trigger
                document.getElementById('solveBtn').innerText = "ALL LESSONS COMPLETE!";
                document.getElementById('solveBtn').style.background = "#ffd700";
                document.getElementById('solveBtn').style.color = "#000";
                
                setTimeout(() => {
                    window.location.href = "{{ site.baseurl }}/chess/final-congrats/";
                }, 1500);
            } else {
                // Return to selection for next box
                alert("Mastery achieved! Returning to selection for your next challenge.");
                setTimeout(() => {
                    window.location.href = "{{ site.baseurl }}/chess/selection/";
                }, 500);
            }
        }

        function updateUI(count) {
            const fill = document.getElementById('progressFill');
            const label = document.getElementById('progressLabel');
            const percentage = (count / 3) * 100;
            
            fill.style.width = percentage + "%";
            label.innerText = "Course Progress: " + count + "/3 Lessons Complete";
        }

        window.onload = function() {
            const data = JSON.parse(localStorage.getItem('chessItinerary'));
            const progress = JSON.parse(localStorage.getItem('chessProgress')) || { completedCount: 0 };
            
            if (!data) {
                window.location.href = "{{ site.baseurl }}/chess/";
                return;
            }

            // Sync User Stats
            document.getElementById('userDisplay').innerText = data.user + " [" + data.level + "]";
            updateUI(progress.completedCount);

            const module = data.selectedModule;
            const piece = data.style;
            
            // THE 9 MODULE PUZZLE ENGINE
            const themes = {
                "Piece Movement": { desc: "Master the basics! Find the safest way to capture your opponent's undefended pieces.", theme: "oneMove" },
                "Board Anatomy": { desc: "Vision is key. Identify the squares that give you the most control over the board.", theme: "advantage" },
                "First Checkmate": { desc: "The finishing blow. Look for the move that traps the enemy King with no escape.", theme: "mateIn1" },
                "Scholar's Mate": { desc: "A classic opening trap. Attack the weak f7 pawn and end the game early!", theme: "mateIn2" },
                "Tactical Forks": { desc: "Double pressure. Use one piece to attack two targets at the same time.", theme: "fork" },
                "Castling Rules": { desc: "Defense first. Secure your King's safety while developing your Rooks.", theme: "kingsideCastle" },
                "Positional Play": { desc: "Strategic maneuvering. Improve your piece placement to squeeze your opponent.", theme: "crushing" },
                "Endgame Grinds": { desc: "The final showdown. Use your King and remaining pawns to promote to a Queen.", theme: "endgame" },
                "Sicilian Defense": { desc: "Black's sharpest weapon. Find the tactical counter-punch in this aggressive opening.", theme: "opening" }
            };

            const config = themes[module] || themes["Piece Movement"];
            
            document.getElementById('moduleTitle').innerText = module;
            document.getElementById('moduleContent').innerText = config.desc;
            document.getElementById('advisorTip').innerText = `Advisor Tip: Your favorite piece, the ${piece}, is your best tool for this lesson!`;
            
            // Load Functional Lichess Frame
            document.getElementById('puzzleFrame').src = `https://lichess.org/training/frame?theme=${config.theme}&bg=dark`;
        };
    </script>
</body>
</html>