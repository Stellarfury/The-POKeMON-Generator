<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TPG Ultimate (Definitive Build)</title>
    <style>
/* TPG Ultimate - style.css (Definitive Build) */

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap');

:root {
    --color-dark-primary: #121212;
    --color-dark-secondary: #232323;
    --color-glass-bg: rgba(44, 44, 44, 0.6);
    --color-glass-border: rgba(255, 255, 255, 0.15);
    --color-text-primary: #f0f0f0;
    --color-text-secondary: #b3b3b3;
    --color-accent: #3a7eff;
    --color-accent-glow: rgba(58, 126, 255, 0.7);
    --color-gold: #ffd700;
    --color-purple: #9370db;
    --color-red: #ff4d4d;
    --color-rainbow: linear-gradient(45deg, red, orange, yellow, green, blue, indigo, violet);
    --sidebar-width: 250px;
    --border-radius: 12px;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
    font-family: 'Poppins', sans-serif;
    background-image: linear-gradient(135deg, var(--color-dark-secondary), var(--color-dark-primary));
    color: var(--color-text-primary);
    overflow: hidden;
    height: 100vh;
    width: 100vw;
    transition: background-image 0.5s ease-in-out;
}

.app-container { display: flex; height: 100vh; width: 100%; }
#sidebar { width: var(--sidebar-width); height: 100%; background: rgba(0, 0, 0, 0.2); display: flex; flex-direction: column; padding: 20px; border-right: 1px solid var(--color-glass-border); flex-shrink: 0; }
#main-content { flex-grow: 1; height: 100%; overflow-y: auto; padding: 30px; position: relative; }

/* --- Sidebar --- */
.game-title { text-align: center; font-size: 2.5rem; margin-bottom: 20px; text-shadow: 0 0 10px var(--color-accent-glow); }
#main-nav { display: flex; flex-direction: column; gap: 10px; margin-top: 20px; }
.nav-button { width: 100%; padding: 12px; background: transparent; border: 1px solid var(--color-glass-border); border-radius: var(--border-radius); color: var(--color-text-secondary); font-size: 1rem; font-weight: 600; text-align: left; cursor: pointer; transition: all 0.3s ease; }
.nav-button:hover { background: var(--color-accent); color: var(--color-text-primary); border-color: var(--color-accent); }
.nav-button.active { background: var(--color-accent); color: var(--color-text-primary); box-shadow: 0 0 15px var(--color-accent-glow); border-color: var(--color-accent); }
.sidebar-footer { margin-top: auto; text-align: center; color: var(--color-text-secondary); font-size: 0.8rem; }

/* --- General Page & UI Component Styles --- */
.page { width: 100%; animation: fadeIn 0.5s ease-in-out; }
.page.hidden { display: none; }
.page-header { margin-bottom: 25px; display: flex; justify-content: space-between; align-items: center; }
.page-header h2 { font-size: 2rem; color: var(--color-text-primary); }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

.glass-container { background: var(--color-glass-bg); backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px); border: 1px solid var(--color-glass-border); border-radius: var(--border-radius); padding: 25px; margin-bottom: 20px; }
input, select { width: 100%; padding: 12px; background: rgba(0, 0, 0, 0.3); border: 1px solid var(--color-glass-border); border-radius: 8px; color: var(--color-text-primary); font-size: 1rem; }
button { padding: 12px 20px; background: var(--color-accent); border: none; border-radius: 8px; color: var(--color-text-primary); font-size: 1rem; font-weight: 600; cursor: pointer; transition: all 0.3s ease; }
button:hover:not(:disabled) { box-shadow: 0 0 15px var(--color-accent-glow); filter: brightness(1.2); }
button:disabled { background: #555; cursor: not-allowed; opacity: 0.6; }

#register-form { display: flex; gap: 10px; }
#register-form input { margin-bottom: 0; }
#start-game-prompt-button { width: 100%; }

/* --- 3D DICE STYLES --- */
#dice-container { display: flex; justify-content: center; gap: 40px; margin: 50px 0; perspective: 1000px; height: 80px; }
.dice-cube { width: 80px; height: 80px; position: relative; transform-style: preserve-3d; }
.dice-cube.rolling { animation: dice-roll 1.5s ease-out; }
.dice-cube .face { position: absolute; width: 80px; height: 80px; background: #f0f0f0; border: 2px solid #333; display: flex; justify-content: center; align-items: center; font-size: 2.5rem; font-weight: bold; color: #333; }
.face.front  { transform: rotateY(  0deg) translateZ(40px); } .face.back   { transform: rotateY(180deg) translateZ(40px); }
.face.right  { transform: rotateY( 90deg) translateZ(40px); } .face.left   { transform: rotateY(-90deg) translateZ(40px); }
.face.top    { transform: rotateX( 90deg) translateZ(40px); } .face.bottom { transform: rotateX(-90deg) translateZ(40px); }
@keyframes dice-roll { 100% { transform: rotateX(1440deg) rotateY(1080deg) rotateZ(720deg); } }

/* --- Roll Page Elements --- */
#roll-button { display: block; margin: 0 auto; width: 200px; padding: 15px; font-size: 1.2rem; }
#turn-summary { text-align: center; font-size: 1.5rem; font-weight: bold; margin-top: 20px; height: 30px; transition: opacity 0.5s; opacity: 0; }
#roll-results-container { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; margin-top: 30px; }

/* --- REVEAL ANIMATIONS & CARD STYLES --- */
.pokemon-card { background: linear-gradient(145deg, #444, #333); border: 2px solid var(--color-glass-border); border-radius: var(--border-radius); padding: 15px; text-align: center; box-shadow: inset 0 0 10px rgba(0,0,0,0.5); position: relative; overflow: hidden; transform: scale(0); animation: pop-in 0.5s ease forwards; }
@keyframes pop-in { to { transform: scale(1); } }
.pokemon-card img { width: 96px; height: 96px; image-rendering: pixelated; filter: drop-shadow(0 4px 6px rgba(0,0,0,0.4)); transition: transform 0.3s ease; }
.pokemon-card:hover img { transform: scale(1.1); }
.pokemon-card-name { font-weight: 600; margin-top: 10px; }
.pokemon-card-tags { min-height: 20px; margin-top: 5px; display: flex; flex-wrap: wrap; justify-content: center; gap: 5px; }
.tag { background-color: var(--color-accent); font-size: 0.7rem; padding: 2px 8px; border-radius: 10px; font-weight: 600; }

.reveal-overlay { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border-radius: inherit; z-index: 2; pointer-events: none; }
.pokemon-card.rarity-shiny .reveal-overlay { animation: shiny-reveal 1.5s forwards; }
.pokemon-card.rarity-secret .reveal-overlay { animation: secret-reveal 1s forwards; }
.pokemon-card.rarity-rainbow .reveal-overlay { animation: rainbow-reveal 1.5s forwards; }
.pokemon-card.type-gmax { animation: gmax-reveal 4s ease-in-out infinite 1.5s; }
.pokemon-card.type-legendary { animation: legendary-reveal 5s ease-in-out infinite 1.5s; }
@keyframes shiny-reveal { 0% { box-shadow: inset 0 0 40px 20px rgba(255,215,0,0); } 50% { box-shadow: inset 0 0 40px 20px rgba(255,215,0,0.8); } 100% { box-shadow: inset 0 0 40px 20px rgba(255,215,0,0); } }
@keyframes secret-reveal { from { background: radial-gradient(circle at center, rgba(147, 112, 219, 0.5) 0%, transparent 10%); transform: scale(0); } to { background: radial-gradient(circle at center, rgba(147, 112, 219, 0) 70%, transparent 100%); transform: scale(2.5); } }
@keyframes rainbow-reveal { 0%,100% { box-shadow: 0 0 20px 5px red; } 20% { box-shadow: 0 0 20px 5px orange; } 40% { box-shadow: 0 0 20px 5px yellow; } 60% { box-shadow: 0 0 20px 5px green; } 80% { box-shadow: 0 0 20px 5px blue; } }
@keyframes gmax-reveal { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }
@keyframes legendary-reveal { 0%, 100% { filter: drop-shadow(0 0 3px white); } 50% { filter: drop-shadow(0 0 15px white); } }

/* --- TROPHY CASE --- */
#trophy-display-area { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 25px; }
.trophy-card { padding: 10px; text-align: center; position: relative; overflow: hidden; border-radius: var(--border-radius); display: flex; flex-direction: column; align-items: center; justify-content: flex-start; width: 100%; aspect-ratio: 63 / 88; border: 2px solid rgba(255, 255, 255, 0.3); }
.trophy-card img { width: 85%; height: auto; flex-grow: 1; object-fit: contain; margin-bottom: 5px; }
.trophy-card .pokemon-card-name { font-weight: 600; width: 100%; padding: 5px; background-color: rgba(0, 0, 0, 0.2); }
.trophy-card .trophy-rarity-label { position: absolute; top: 10px; left: 10px; background: rgba(0,0,0,0.5); padding: 3px 8px; border-radius: 20px; font-size: 0.8rem; font-weight: bold; color: var(--color-text-primary); z-index: 1; }
.trophy-card.rarity-shiny { background: radial-gradient(circle, #fde497, var(--color-gold)); color: #333; }
.trophy-card.rarity-secret { background: radial-gradient(circle, #c4a9ff, var(--color-purple)); color: var(--color-text-primary); }
.trophy-card.rarity-rainbow { background: var(--color-rainbow); animation: rainbow-bg 4s linear infinite; background-size: 200% 200%; color: #333; }
@keyframes rainbow-bg { to { background-position: 200%; } }

/* --- EVENT & ODDS UI STYLES --- */
#event-indicator { padding: 10px; text-align: center; }
#odds-display { position: fixed; bottom: 10px; right: 10px; z-index: 50; padding: 10px 15px; border-radius: var(--border-radius); background: var(--color-glass-bg); backdrop-filter: blur(10px); border: 1px solid var(--color-glass-border); text-align: right; font-size: 0.9rem; transition: opacity 0.5s; }
#odds-display .event-title { font-weight: bold; }
#event-notification-banner { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); padding: 15px 30px; border-radius: var(--border-radius); color: var(--color-text-primary); font-size: 1.2rem; font-weight: bold; z-index: 1001; text-align: center; background: var(--color-glass-bg); backdrop-filter: blur(10px); border: 1px solid var(--color-glass-border); animation: slideDownFade 5s forwards; visibility: hidden; }
#event-notification-banner.visible { visibility: visible; }
.event-flavor-text { font-style: italic; font-size: 1rem; display: block; }
@keyframes slideDownFade { 0% { top: -120px; opacity: 0; } 10% { top: 20px; opacity: 1; } 90% { top: 20px; opacity: 1; } 100% { top: -120px; opacity: 0; } }
body.event-eclipse { background-image: linear-gradient(135deg, #4c2a85, #1d1135); }
body.event-rainbow { background-image: var(--color-rainbow); background-size: 400% 400%; animation: rainbow-bg 8s ease infinite; }
body.event-flare { background-image: linear-gradient(135deg, #ff4500, #8b0000); }
body.event-glacial { background-image: linear-gradient(135deg, #add8e6, #4682b4); }
body.event-celestial { background-image: linear-gradient(135deg, #0f0c29, #302b63, #24243e); }

/* --- DEV PANEL --- */
#dev-panel.hidden { display: none; }
.dev-panel-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; }
.dev-group h3 { margin-bottom: 15px; }
.dev-group input, .dev-group select { margin-bottom: 10px; }
.dev-group button { width: 100%; margin-bottom: 10px; }
#wipe-data-btn { background-color: var(--color-red); }

/* --- MISC & MODALS --- */
.player-list-item { display: flex; justify-content: space-between; align-items: center; padding: 12px; border-bottom: 1px solid var(--color-glass-border); }
.player-list-item:last-child { border-bottom: none; }
.delete-player-btn { background: none; border: none; color: var(--color-red); font-size: 1.2rem; cursor: pointer; padding: 5px; }
#scoreboard-table { width: 100%; border-collapse: collapse; }
#scoreboard-table th, #scoreboard-table td { padding: 15px; text-align: left; border-bottom: 1px solid var(--color-glass-border); }
.titles-container { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.titles-container ul { list-style: none; padding-left: 0; }
.titles-container li { padding: 10px; margin-bottom: 8px; border: 1px solid var(--color-glass-border); border-radius: 8px; cursor: pointer; transition: all 0.2s ease; }
.titles-container li.unlocked:hover { background-color: var(--color-accent); }
.titles-container li.equipped { background-color: var(--color-gold); color: var(--color-dark-primary); border-color: var(--color-gold); }
.titles-container li.locked { opacity: 0.5; cursor: not-allowed; }
.modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.7); backdrop-filter: blur(5px); display: flex; justify-content: center; align-items: center; z-index: 1000; animation: fadeIn 0.3s; }
.modal-overlay.hidden { display: none; }
.modal-content { width: 90%; max-width: 500px; }
#start-game-player-checklist { text-align: left; max-height: 200px; overflow-y: auto; margin-bottom: 20px; border: 1px solid var(--color-glass-border); padding: 10px; border-radius: 8px; }
#start-game-player-checklist label { display: block; margin-bottom: 10px; cursor: pointer; }
#start-game-player-checklist input { margin-right: 10px; }
</style>
</head>
<body>
    <!-- Main Application Container -->
    <div class="app-container">

        <!-- Sidebar Navigation -->
        <aside id="sidebar">
            <h1 class="game-title">TPG</h1>
            <div id="event-indicator" class="glass-container">
                <!-- Event status will be rendered here -->
            </div>
            <nav id="main-nav">
                <button class="nav-button active" data-page="roll">Roll</button>
                <button class="nav-button" data-page="trophy-case">Trophy Case</button>
                <button class="nav-button" data-page="scoreboard">Scoreboard</button>
                <button class="nav-button" data-page="titles">Titles</button>
                <button class="nav-button" data-page="register">Register</button>
                <button class="nav-button" data-page="dev">Dev</button>
            </nav>
            <div class="sidebar-footer">
                <p>PC Ultimate Edition v1.0</p>
            </div>
        </aside>

        <!-- Main Content Area -->
        <main id="main-content">
            <!-- Roll Page -->
            <section id="page-roll" class="page">
                <div class="page-header"><h2 id="current-turn-display">Create players to begin...</h2></div>
                <div id="dice-container">
                    <div class="dice-cube" id="die-1"><div class="face front">1</div><div class="face back">6</div><div class="face right">3</div><div class="face left">4</div><div class="face top">2</div><div class="face bottom">5</div></div>
                    <div class="dice-cube" id="die-2"><div class="face front">1</div><div class="face back">6</div><div class="face right">3</div><div class="face left">4</div><div class="face top">2</div><div class="face bottom">5</div></div>
                    <div class="dice-cube" id="die-3"><div class="face front">1</div><div class="face back">6</div><div class="face right">3</div><div class="face left">4</div><div class="face top">2</div><div class="face bottom">5</div></div>
                    <div class="dice-cube" id="die-4"><div class="face front">1</div><div class="face back">6</div><div class="face right">3</div><div class="face left">4</div><div class="face top">2</div><div class="face bottom">5</div></div>
                    <div class="dice-cube" id="die-5"><div class="face front">1</div><div class="face back">6</div><div class="face right">3</div><div class="face left">4</div><div class="face top">2</div><div class="face bottom">5</div></div>
                </div>
                <button id="roll-button" disabled>Roll Dice</button>
                <div id="turn-summary"></div>
                <div id="roll-results-container"></div>
            </section>

            <!-- Trophy Case Page -->
            <section id="page-trophy-case" class="page hidden">
                <div class="page-header"><h2>Trophy Case</h2><select id="trophy-player-select"></select></div>
                <div id="trophy-display-area" class="glass-container"></div>
            </section>

            <!-- Scoreboard Page -->
            <section id="page-scoreboard" class="page hidden">
                <div class="page-header"><h2>Scoreboard</h2></div>
                <div id="scoreboard-container" class="glass-container">
                    <table id="scoreboard-table">
                        <thead>
                            <tr>
                                <th>Player</th>
                                <th>Title</th>
                                <th>Current Score</th>
                                <th>Total Wins</th>
                                <th>Trophies</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Player scores will be inserted here by JS -->
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- Titles Page -->
            <section id="page-titles" class="page hidden">
                <div class="page-header"><h2>Titles & Achievements</h2><select id="titles-player-select"></select></div>
                <div class="titles-container">
                    <div class="glass-container">
                        <h3>Trophy Titles</h3>
                        <ul id="trophy-titles-list">
                            <!-- Trophy titles will be inserted here by JS -->
                        </ul>
                    </div>
                    <div class="glass-container">
                        <h3>Win Titles</h3>
                        <ul id="win-titles-list">
                            <!-- Win titles will be inserted here by JS -->
                        </ul>
                    </div>
                </div>
            </section>
            
            <!-- Register Page -->
            <section id="page-register" class="page hidden">
                 <div class="page-header"><h2>Register Players</h2></div>
                <div class="glass-container">
                    <form id="register-form">
                        <input type="text" id="player-name-input" placeholder="Enter new player name" required autocomplete="off">
                        <button type="submit">Create Player</button>
                    </form>
                </div>
                <div class="glass-container">
                    <h3>Registered Players</h3>
                    <div id="player-list">
                        <!-- Player list will be inserted here by JS -->
                    </div>
                </div>
                <div class="glass-container">
                    <button id="start-game-prompt-button">Start New Game</button>
                </div>
            </section>

            <!-- Developer Page -->
            <section id="page-dev" class="page hidden">
                 <!-- This entire section is hidden, JS will reveal the panel inside -->
                <div id="dev-panel" class="hidden">
                    <div class="page-header"><h2>Developer Panel</h2></div>
                    <div class="dev-panel-grid">
                        <div class="glass-container dev-group">
                            <h3>Cosmic Events (Toggle)</h3>
                            <button class="dev-button" data-event-key="ECLIPSE">Toggle Eclipse 🌑</button>
                            <button class="dev-button" data-event-key="RAINBOW">Toggle Rainbow Burst 🌈</button>
                            <button class="dev-button" data-event-key="FLARE">Toggle Flare Storm 🔥</button>
                            <button class="dev-button" data-event-key="GLACIAL">Toggle Glacial Era 🧊</button>
                            <button class="dev-button" data-event-key="CELESTIAL">Toggle Celestial Gateway 🌌</button>
                        </div>
                       
<!-- PASTE THIS NEW BLOCK IN ITS PLACE -->
<div class="glass-container dev-group">
    <h3>Force Generation # The-POKEMON-Generator
