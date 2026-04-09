---
layout: post
title: "Grandmaster Graduation"
permalink: /chess/final-congrats/
---

<html lang="en">
<head>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        /* THE VISUAL ENGINE: Flying Pieces & Background */
        body { 
            margin: 0; padding: 0; height: 100vh;
            background: radial-gradient(circle, #2c3e50 0%, #000000 100%);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            font-family: 'Segoe UI', Tahoma, sans-serif; overflow: hidden; color: white;
            position: relative;
        }

        /* THE FLYING KNIGHT (Your Branding) */
        .flying-knight {
            position: absolute;
            font-size: 5rem;
            animation: fly 10s linear infinite;
            opacity: 0.2;
            z-index: 1;
        }

        @keyframes fly {
            0% { left: -10%; top: 20%; transform: rotate(0deg); }
            50% { top: 50%; }
            100% { left: 110%; top: 20%; transform: rotate(360deg); }
        }

        /* FALLING PIECES */
        .falling-piece {
            position: absolute;
            top: -10%;
            font-size: 2rem;
            opacity: 0.3;
            animation: fall linear infinite;
            z-index: 1;
        }

        @keyframes fall {
            to { transform: translateY(110vh) rotate(360deg); }
        }

        /* THE TROPHY & UI (Front Layer) */
        .content-wrap {
            position: relative;
            z-index: 10;
            text-align: center;
            background: rgba(0, 0, 0, 0.6);
            padding: 50px;
            border-radius: 25px;
            border: 2px solid #ffd700;
            backdrop-filter: blur(10px);
            box-shadow: 0 0 50px rgba(255, 215, 0, 0.2);
        }

        .trophy { 
            font-size: 150px; 
            margin-bottom: 20px;
            display: inline-block;
            filter: drop-shadow(0 0 20px #ffd700);
            animation: pulse 2s infinite alternate;
        }

        @keyframes pulse { from { transform: scale(1); } to { transform: scale(1.1); } }

        h1 { color: #ffd700; font-size: 3.5rem; margin: 0; letter-spacing: 4px; }
        
        .stats { font-size: 1.2rem; margin: 20px 0; color: #ccc; }
        .stats b { color: #ffd700; }

        .btn-home { 
            display: inline-block; margin-top: 30px; padding: 18px 45px; 
            background: #ffd700; color: #1a1a1a; text-decoration: none; 
            font-weight: bold; font-size: 1.3rem; border-radius: 50px; 
            transition: 0.3s;
        }
        .btn-home:hover { transform: scale(1.1); background: white; box-shadow: 0 0 30px #ffd700; }
    </style>
</head>
<body>

    <div class="flying-knight">♘</div>
    <div id="falling-container"></div>

    <div class="content-wrap">
        <div class="trophy">🏆</div>
        <h1>COURSE COMPLETE</h1>
        <div class="stats" id="finalStats">
            Training validated for <b>User</b><br>
            Rank attained: <b>Grandmaster</b>
        </div>
        <a href="{{ site.baseurl }}/chess/" class="btn-home" onclick="resetGame()">RESTART CAREER</a>
    </div>

    <script>
        function resetGame() {
            // Clears the progress counter so the next run-through starts at 0/3
            localStorage.setItem('chessProgress', JSON.stringify({ completedCount: 0 }));
        }

        window.onload = function() {
            const data = JSON.parse(localStorage.getItem('chessItinerary'));
            if (data) {
                document.getElementById('finalStats').innerHTML = `
                    Student: <b>${data.user}</b><br>
                    Level Mastered: <b>${data.level}</b><br>
                    Style: <b>${data.style} Specialist</b>
                `;
            }

            // Create falling chess pieces
            const container = document.getElementById('falling-container');
            const pieces = ['♟', '♞', '♝', '♜', '♛', '♚'];
            for (let i = 0; i < 20; i++) {
                let p = document.createElement('div');
                p.className = 'falling-piece';
                p.innerText = pieces[Math.floor(Math.random() * pieces.length)];
                p.style.left = Math.random() * 100 + 'vw';
                p.style.animationDuration = (Math.random() * 5 + 5) + 's';
                p.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(p);
            }

            // Infinite Confetti loop
            var duration = 15 * 1000;
            var animationEnd = Date.now() + duration;
            var defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            function randomInRange(min, max) { return Math.random() * (max - min) + min; }

            var interval = setInterval(function() {
                var timeLeft = animationEnd - Date.now();
                if (timeLeft <= 0) return clearInterval(interval);
                var particleCount = 50 * (timeLeft / duration);
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
            }, 250);
        };
    </script>
</body>
</html>