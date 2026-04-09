---
layout: post
title: "How to Move Pieces"
permalink: /chess/HTMP/
---

<style>
    html, body { 
        background-color: #1e391a !important; 
        margin: 0; 
        padding: 0;
        font-family: 'Georgia', serif;
    }

    .chess-wrapper {
        display: flex;
        justify-content: center;
        padding: 40px 20px;
    }

    .info-card {
        background: rgba(0, 0, 0, 0.9);
        color: white !important;
        padding: 50px;
        border-radius: 15px;
        border: 2px solid #ffd700;
        max-width: 800px;
        box-shadow: 0 15px 50px rgba(0,0,0,0.8);
    }

    h1, h2 { 
        color: #ffd700 !important; 
        text-align: center;
        border-bottom: 1px solid rgba(255, 215, 0, 0.3);
        padding-bottom: 10px;
    }

    .piece-title {
        color: #ffd700;
        font-weight: bold;
        display: block;
        margin-top: 20px;
        font-size: 1.2rem;
    }

    p {
        line-height: 1.8;
        font-size: 1.1rem;
        color: #ffffff !important;
        margin-bottom: 15px;
        text-align: justify;
    }

    .gold-btn {
        display: inline-block;
        margin-top: 30px;
        background: #ffcc00;
        color: #1e391a !important;
        padding: 15px 30px;
        border-radius: 50px;
        text-decoration: none;
        font-weight: bold;
        text-transform: uppercase;
        transition: 0.3s;
        border: 1px solid #ffd700;
    }

    .gold-btn:hover {
        background: #ffffff;
        transform: scale(1.05);
    }
</style>

<div class="chess-wrapper">
    <div class="info-card">
        <h1>♟ How to Move Pieces</h1>
        
        <p>
            This module provides a comprehensive guide to the unique mechanical capabilities of each chess piece, ensuring a complete understanding of how to navigate the board with precision. The curriculum details the specific movement patterns and capture rules for every unit, ranging from the foundational pawn to the multifaceted queen. By mastering these essential mechanics, a student establishes the necessary groundwork for executing the complex strategies and tactical maneuvers presented in the advanced training sections.
        </p>

        <h2>The Pieces</h2>

        <span class="piece-title">The Pawn:</span>
        <p>This unit advances one square forward at a time, though it maintains the unique privilege of moving two squares on its initial departure from the starting rank. It captures exclusively on the forward diagonals and is the only piece capable of "Promotion," where reaching the furthest rank allows it to transform into any other piece, typically the Queen.</p>

        <span class="piece-title">The Rook:</span>
        <p>Operating as a heavy long-range power, the rook traverses any number of squares horizontally or vertically. It is instrumental in the "Castling" maneuver, a special rule where the King and Rook move toward each other to secure the King’s safety and activate the Rook for battle.</p>

        <span class="piece-title">The Knight:</span>
        <p>This piece utilizes an unorthodox "L-shaped" displacement—moving two squares in one cardinal direction and one square perpendicularly. It is the only unit on the board with the ability to leap over other pieces, making it an essential tool for navigating congested positions and delivering sudden, unavoidable checks.</p>

        <span class="piece-title">The Bishop:</span>
        <p>Confined to the color of its starting square, the bishop travels any distance diagonally across the board. Because it requires open pathways to be effective, its strength increases significantly as the board clears during the midgame and endgame phases.</p>

        <span class="piece-title">The Queen:</span>
        <p>As the most formidable asset in a player’s arsenal, the queen combines the movement profiles of both the rook and the bishop. She can move any number of squares in any straight or diagonal direction, allowing her to dominate multiple sectors of the board simultaneously.</p>

        <span class="piece-title">The King:</span>
        <p>The king is the most vital piece, as its capture results in the immediate conclusion of the match. While limited to moving only one square in any direction, the king must be protected at all costs, and it cannot move into any square where it would be under direct attack by an opponent's piece.</p>

        <h2>Essential Rules</h2>

        <p><strong>Check and Checkmate:</strong> A King is in "Check" when it is under direct attack; the player must immediately move the King, block the path, or capture the attacker. "Checkmate" occurs when the King is in check and there are no legal moves to escape, ending the game.</p>

        <p><strong>En Passant:</strong> A specialized pawn capture that occurs when a pawn moves two squares forward from its starting position and lands horizontally adjacent to an opponent's pawn. The opponent may capture that pawn "in passing" as if it had only moved one square.</p>

        <p><strong>Stalemate:</strong> This occurs when a player is not in check but has no legal moves remaining. In this scenario, the game results in a technical draw, regardless of which player has more pieces remaining on the board.</p>

        <div style="text-align: center;">
            <a href="{{site.baseurl}}/chess/helper/" class="gold-btn">
                ← Back to Registration
            </a>
        </div>
    </div>
</div>