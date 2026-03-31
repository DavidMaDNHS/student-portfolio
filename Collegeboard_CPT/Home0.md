---
layout: post
title: "Chess"
description: "Improve at chess with our interactive tools."
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

        /* Increased z-index to ensure text and buttons are clickable */
        .container {
            text-align: center;
            padding: 20px;
            position: relative;
            z-index: 100; 
            width: 100%;
            max-width: 600px;
        }

        .pieces-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none; /* Prevents background pieces from blocking clicks */
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
            margin-bottom: 30px;
        }

        .start-button:hover {
            transform: scale(1.1);
            box-shadow: 0 0 30px gold;
        }

        /* Suggestions Box Styling */
        #microblog-container {
            background: rgba(0, 0, 0, 0.6);
            padding: 20px;
            border-radius: 15px;
            border: 1px solid #ffd700;
            text-align: left;
            backdrop-filter: blur(10px);
            margin-top: 20px;
        }

        .blog-header {
            color: #ffd700;
            margin-bottom: 15px;
            font-size: 1.2rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            display: flex;
            justify-content: space-between;
        }

        .blog-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        #blogInput {
            flex-grow: 1;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #ffd700;
            background: rgba(255, 255, 255, 0.95);
            font-family: inherit;
            color: #333;
        }

        #postBtn {
            background: #ffd700;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            color: #1e391a;
        }

        #commentList {
            max-height: 150px;
            overflow-y: auto;
            border-top: 1px solid rgba(255, 215, 0, 0.2);
        }

        .knight-rider {
            position: fixed;
            bottom: 50px;
            font-size: 4rem;
            animation: drive 12s linear infinite;
            z-index: 5;
            color: #ffd700;
            filter: drop-shadow(0 5px 10px rgba(0, 0, 0, 0.5));
            pointer-events: none;
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

        <div id="microblog-container">
            <div class="blog-header">
                <span>Suggestions</span>
                <span id="clearNotes" style="font-size: 0.7rem; cursor: pointer; text-decoration: underline; opacity: 0.7;">Clear All</span>
            </div>
            
            <div class="blog-input-group">
                <input type="text" id="blogInput" placeholder="Log a suggestion...">
                <button id="postBtn">Post</button>
            </div>

            <div id="commentList"></div>
        </div>
    </div>

    <script>
        // Falling Pieces Logic
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

        // Suggestions Logic
        const blogInput = document.getElementById('blogInput');
        const postBtn = document.getElementById('postBtn');
        const commentList = document.getElementById('commentList');
        const clearBtn = document.getElementById('clearNotes');

        window.onload = () => {
            const saved = JSON.parse(localStorage.getItem('chessSuggestions')) || [];
            saved.forEach(note => renderNote(note.text, note.time));
        };

        function renderNote(text, time) {
            const div = document.createElement('div');
            div.style.padding = "10px 0";
            div.style.borderBottom = "1px solid rgba(255,215,0,0.1)";
            div.style.display = "flex";
            div.style.justifyContent = "space-between";
            div.innerHTML = `<span style="color:white; font-size:0.9rem;">${text}</span>
                             <small style="color:#ffd700; opacity:0.6;">${time}</small>`;
            commentList.prepend(div);
        }

        postBtn.onclick = () => {
            const val = blogInput.value.trim();
            if(!val) return;
            const time = new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
            renderNote(val, time);
            
            const saved = JSON.parse(localStorage.getItem('chessSuggestions')) || [];
            saved.push({text: val, time: time});
            localStorage.setItem('chessSuggestions', JSON.stringify(saved));
            blogInput.value = "";
        };

        blogInput.onkeypress = (e) => { if(e.key === "Enter") postBtn.click(); };

        clearBtn.onclick = () => {
            if(confirm("Clear all suggestions?")) {
                localStorage.removeItem('chessSuggestions');
                commentList.innerHTML = "";
            }
        };
    </script>
</body>
</html>