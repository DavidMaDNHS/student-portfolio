---
layout: post
title: "Overview"
permalink: /chess/overview/
---

<style>
    html, body { 
        background-color: #1e391a !important; 
        margin: 0; 
        padding: 0;
        font-family: 'Georgia', serif;
        height: 100%;
    }

    .chess-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 80vh;
        padding: 20px;
    }

    .info-card {
        background: rgba(0, 0, 0, 0.9);
        color: white !important;
        padding: 50px;
        border-radius: 15px;
        border: 2px solid #ffd700;
        max-width: 700px;
        box-shadow: 0 15px 50px rgba(0,0,0,0.8);
        text-align: center;
    }

    h1 { 
        color: #ffd700 !important; 
        font-size: 2.5rem; 
        margin-bottom: 25px;
        border-bottom: 1px solid rgba(255, 215, 0, 0.3);
        padding-bottom: 15px;
    }

    p {
        line-height: 1.8;
        font-size: 1.15rem;
        margin-bottom: 30px;
        text-align: justify;
        color: #ffffff !important;
    }

    .gold-btn {
        display: inline-block;
        background: #ffcc00;
        color: #1e391a !important;
        padding: 15px 30px;
        border-radius: 50px;
        font-weight: bold;
        text-decoration: none;
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
        <h1>♟ Academy Overview</h1>

        <p>
            This interactive chess academy is designed to provide a structured learning path for players of all skill levels, from beginners to experts. Users may register and authenticate to access specialized training modules covering the full spectrum of play, from fundamental piece mechanics to advanced endgame theory. By selecting a personalized skill level, the curriculum is tailored to ensure every student encounters the appropriate challenges necessary to refine their strategic execution and improve their overall game.
        </p>

        <a href="{{site.baseurl}}/chess/helper/" class="gold-btn">
            ← Back to Registration
        </a>
    </div>
</div>