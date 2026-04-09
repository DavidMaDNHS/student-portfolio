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
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body { 
            font-family: 'Georgia', serif; 
            overflow-x: hidden; 
            background: #2d5a27; 
            min-height: 100vh; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
        }

        .bg-gradient {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #3d7a36 0%, #244d1f 100%);
            z-index: -1;
        }

        /* SIDEBAR & STEEL BLUE CLOSE BUTTON */
        #contactSidebar { 
            position: fixed; 
            left: -320px; 
            top: 0; 
            width: 300px; 
            height: 100%; 
            background: rgba(0, 0, 0, 0.98); 
            border-right: 2px solid #ffd700; 
            transition: 0.4s; 
            z-index: 9999; 
            padding: 25px; 
            display: flex; 
            flex-direction: column; 
        }
        #contactSidebar.active { left: 0; }
        
        .close-contact { 
            background: #4682B4 !important; 
            color: white !important; 
            padding: 14px; 
            text-align: center; 
            cursor: pointer; 
            font-weight: bold; 
            border-radius: 8px; 
            margin-top: 70px; 
            margin-bottom: 30px; 
            border: 1px solid rgba(255,255,255,0.3); 
            text-transform: uppercase; 
        }

        .contact-toggle { position: fixed; left: 0; top: 50%; transform: translateY(-50%); background: #ffd700; color: #1e391a; padding: 15px 10px; cursor: pointer; border-radius: 0 10px 10px 0; font-weight: bold; z-index: 1500; writing-mode: vertical-rl; text-orientation: mixed; }

        /* MAIN UI */
        .container { text-align: center; z-index: 100; width: 100%; max-width: 600px; }
        h1 { font-size: 5rem; color: #ffd700; margin-bottom: 10px; letter-spacing: 0.1em; text-shadow: 2px 2px 10px rgba(0,0,0,0.5); }
        .subtitle { font-size: 1.8rem; color: white; margin-bottom: 40px; font-style: italic; }

        /* UPDATED WARM GOLD BUTTON */
        .start-button { 
            display: inline-block; 
            padding: 20px 50px; 
            font-size: 1.5rem; 
            font-weight: bold; 
            color: #1e391a; 
            background: #ffcc00; /* Comfortable Warm Yellow */
            border-radius: 50px; 
            text-decoration: none; 
            transition: all 0.4s ease; 
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            border: 2px solid #ffd700;
        }
        .start-button:hover { 
            transform: scale(1.08); 
            box-shadow: 0 0 25px #ffcc00, 0 0 50px rgba(255, 204, 0, 0.4); 
            background: #ffd700; /* Shifts to the brighter gold, not white */
            color: #000;
        }

        /* SUGGESTIONS LOG */
        #microblog-container { background: rgba(0, 0, 0, 0.85); padding: 20px; border-radius: 15px; border: 1px solid #ffd700; margin-top: 30px; text-align: left; }
        .blog-header { color: #ffd700; font-weight: bold; display: flex; justify-content: space-between; margin-bottom: 15px; }
        .blog-input-group { display: flex; gap: 10px; }
        #blogInput { flex-grow: 1; padding: 12px; border-radius: 5px; border: none; background: white; color: #333; font-weight: bold; }
        #postBtn { padding: 10px 25px; background: #ffd700; border: none; font-weight: bold; cursor: pointer; border-radius: 5px; color: #1e391a; }

        #commentList { max-height: 150px; overflow-y: auto; margin-top: 15px; color: white; }
        .note-item { padding: 8px 0; border-bottom: 1px solid rgba(255,215,0,0.2); display: flex; justify-content: space-between; }

        /* PIECES */
        .pieces-container { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 1; pointer-events: none; }
        .piece { position: absolute; color: rgba(255, 255, 255, 0.2); font-size: 2.5rem; animation: fall linear infinite; }
        @keyframes fall { 0% { transform: translateY(-10vh) rotate(0deg); opacity: 0; } 10% { opacity: 1; } 100% { transform: translateY(110vh) rotate(360deg); opacity: 0; } }
        .knight-rider { position: fixed; bottom: 50px; font-size: 4rem; animation: drive 12s linear infinite; z-index: 5; color: #ffd700; pointer-events: none; }
        @keyframes drive { 0% { left: -100px; } 100% { left: calc(100% + 100px); } }
    </style>
</head>
<body>
    <div class="bg-gradient"></div>
    <div class="contact-toggle" onclick="toggleContact()">CONTACT US</div>
    
    <div id="contactSidebar">
        <div class="close-contact" onclick="toggleContact()">✕ COLLAPSE PANEL</div>
        <h2 style="color:#ffd700; text-align:center; margin-bottom:20px;">Support Hub</h2>
        <form class="contact-form" action="https://formspree.io/f/YOUR_ID" method="POST">
            <input type="email" name="email" placeholder="Your Email" required>
            <textarea name="message" placeholder="Your Message" required style="height: 120px; width:100%; background:#222; color:white; padding:10px; border-radius:5px; margin-bottom:15px; border: 1px solid #444;"></textarea>
            <button type="submit" style="width:100%; padding:15px; background:#ffd700; color:#1e391a; border:none; font-weight:bold; cursor:pointer; border-radius:5px; text-transform:uppercase;">Send Transmission</button>
        </form>
    </div>

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
                <span>Suggestions Log</span>
                <span onclick="clearAll()" style="font-size:0.75rem; cursor:pointer; text-decoration:underline; color:#ffd700;">Clear History</span>
            </div>
            <div class="blog-input-group">
                <input type="text" id="blogInput" placeholder="Log your ideas...">
                <button id="postBtn">Post</button>
            </div>
            <div id="commentList"></div>
        </div>
    </div>

    <script>
        function toggleContact() { document.getElementById('contactSidebar').classList.toggle('active'); }
        
        const pc = document.getElementById('pieces');
        const icons = ['♙', '♘', '♗', '♖', '♕', '♔', '♟', '♞', '♝', '♜', '♛', '♚'];
        for (let i = 0; i < 35; i++) {
            const p = document.createElement('div'); 
            p.className = 'piece'; 
            p.innerText = icons[Math.floor(Math.random() * icons.length)];
            p.style.left = Math.random() * 100 + '%'; 
            p.style.animationDuration = (Math.random() * 8 + 5) + 's'; 
            p.style.animationDelay = (Math.random() * 5) + 's';
            pc.appendChild(p);
        }

        const input = document.getElementById('blogInput');
        const list = document.getElementById('commentList');
        
        function render(text, time) {
            const d = document.createElement('div'); 
            d.className = 'note-item';
            d.innerHTML = `<span>${text}</span> <small style="color:#ffd700; opacity:0.8;">${time}</small>`;
            list.prepend(d);
        }

        document.getElementById('postBtn').onclick = () => {
            const val = input.value.trim();
            if(!val) return;
            const now = new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
            render(val, now);
            const saved = JSON.parse(localStorage.getItem('chessS')) || [];
            saved.push({t: val, d: now});
            localStorage.setItem('chessS', JSON.stringify(saved));
            input.value = "";
        };

        function clearAll() { if(confirm("Clear local suggestions?")) { localStorage.removeItem('chessS'); list.innerHTML = ""; } }
        window.onload = () => { (JSON.parse(localStorage.getItem('chessS')) || []).forEach(n => render(n.t, n.d)); };
    </script>
</body>
</html>