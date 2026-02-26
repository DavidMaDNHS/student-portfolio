---
layout: post
title: "Chess Hub"
description: "Master the board with our interactive tools."
permalink: /chess/
parent: "Chess Project"
footer:
  home: /chess/
  next: /chess/helper/
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chess Cosmos</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            overflow-x: hidden;
            background: linear-gradient(135deg, #2d5a27 0%, #1e391a 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .container {
            text-align: center;
            padding: 20px;
            position: relative;
            z-index: 10;
        }

        .pieces-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }

        .piece {
            position: absolute;
            color: rgba(255, 255, 255, 0.15);
            font-size: 2.5rem;
            user-select: none;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% { transform: translateY(-10vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
        }

        h1 {
            font-size: 5rem;
            font-weight: bold;
            color: #ffd700;
            text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
            margin-bottom: 20px;
            letter-spacing: 0.1em;
        }

        .subtitle {
            font-size: 1.8rem;
            color: #ffffff;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
            margin-bottom: 40px;
            font-style: italic;
        }

        .start-button {
            display: inline-block;
            padding: 20px 50px;
            font-size: 1.5rem;
            font-weight: bold;
            color: #1e391a;
            background: #ffd700;
            border-radius: 50px;
            text-decoration: none;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease;
        }

        .start-button:hover {
            transform: scale(1.1);
            box-shadow: 0 0 30px gold;
        }

        .knight-rider {
            position: fixed;
            bottom: 50px;
            font-size: 4rem;
            animation: drive 12s linear infinite;
            z-index: 5;
            color: #ffd700;
            filter: drop-shadow(0 5px 10px rgba(0, 0, 0, 0.5));
        }

        @keyframes drive {
            0% { left: -100px; }
            100% { left: calc(100% + 100px); }
        }
    </style>
</head>
<body>
    <div class="pieces-container" id="pieces"></div>

    <div class="knight-rider">♞</div> 
    
    <div class="container">
        <h1>CHESS COSMOS</h1>
        <p class="subtitle">Checkmate the Competition</p>
        
        <a href="{{ site.baseurl }}/chess/helper/" class="start-button">
            Start Your Training
        </a>
    </div>

    <script>
        const piecesContainer = document.getElementById('pieces');
        const chessIcons = ['♙', '♘', '♗', '♖', '♕', '♔', '♟', '♞', '♝', '♜', '♛', '♚'];
        
        for (let i = 0; i < 30; i++) {
            const piece = document.createElement('div');
            piece.className = 'piece';
            piece.innerText = chessIcons[Math.floor(Math.random() * chessIcons.length)];
            piece.style.left = Math.random() * 100 + '%';
            piece.style.animationDuration = (Math.random() * 10 + 7) + 's';
            piece.style.animationDelay = (Math.random() * 5) + 's';
            piece.style.fontSize = (Math.random() * 2 + 1) + 'rem';
            piecesContainer.appendChild(piece);
        }
    </script>
</body>
</html>