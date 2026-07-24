<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Movie Imposter Game</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #141e30, #243b55);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
}

.game {
    width: 95%;
    max-width: 500px;
    text-align: center;
}

h1 {
    font-size: 32px;
    margin-bottom: 20px;
}

.card {
    background: rgba(255,255,255,0.12);
    backdrop-filter: blur(10px);
    padding: 30px 20px;
    border-radius: 25px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.4);
}

input {
    width: 90%;
    padding: 15px;
    border: none;
    border-radius: 12px;
    font-size: 18px;
    outline: none;
    margin: 10px;
}

button {
    width: 90%;
    padding: 15px;
    margin: 8px;
    border: none;
    border-radius: 15px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    background: #ffd54f;
    color: #222;
}

button:active {
    transform: scale(0.97);
}

.player-buttons button {
    width: 42%;
    background: white;
}

.hidden {
    display: none;
}

#movieName {
    font-size: 32px;
    font-weight: bold;
    color: #ffd54f;
    margin: 20px 0;
}

#result {
    font-size: 22px;
    margin: 20px 0;
    line-height: 1.5;
}

.error {
    color: #ff7676;
}
</style>
</head>

<body>

<div class="game">

<h1>🎬 MOVIE IMPOSTER</h1>

<div class="card">

<!-- START SCREEN -->
<div id="startScreen">

<h2>4 Player Game</h2>

<p>
Enter a movie name to start the game.
<br>
Four players will take turns viewing their cards.
</p>

<input
id="movieInput"
type="text"
placeholder="Enter Movie Name..."
>

<button onclick="startGame()">
🎮 Start Game
</button>

<p id="error" class="error"></p>

</div>


<!-- PLAYER CARD SCREEN -->
<div id="cardScreen" class="hidden">

<h2 id="playerName"></h2>

<p id="message">
Press the button below to reveal your card.
</p>

<button id="showButton" onclick="showCard()">
👁️ Show My Card
</button>

<button
id="nextButton"
class="hidden"
onclick="nextPlayer()">
📱 Give the phone to the next player
</button>

</div>


<!-- DISCUSSION SCREEN -->
<div id="discussionScreen" class="hidden">

<h2>💬 Discussion Time</h2>

<p>
Each player should give one small hint
about the movie.
</p>

<p>
⚠️ Do not say the movie name directly!
</p>

<p>
🕵️ Find the Imposter!
</p>

<button onclick="showVoting()">
🗳️ Vote Now
</button>

</div>


<!-- VOTING SCREEN -->
<div id="votingScreen" class="hidden">

<h2>🗳️ Who is the Imposter?</h2>

<div class="player-buttons">

<button onclick="vote(0)">Player 1</button>
<button onclick="vote(1)">Player 2</button>
<button onclick="vote(2)">Player 3</button>
<button onclick="vote(3)">Player 4</button>

</div>

<div id="result"></div>

<button
id="restartButton"
class="hidden"
onclick="newGame()">
🔄 New Game
</button>

</div>

</div>

</div>


<script>

let movieName = "";
let imposter = 0;
let currentPlayer = 0;


// START GAME
function startGame() {

    movieName =
    document.getElementById("movieInput")
    .value
    .trim();

    if (movieName === "") {

        document.getElementById("error")
        .innerText =
        "⚠️ Please enter a movie name!";

        return;
    }

    // Choose a random Imposter
    imposter =
    Math.floor(Math.random() * 4);

    currentPlayer = 0;

    document.getElementById("startScreen")
    .classList.add("hidden");

    document.getElementById("discussionScreen")
    .classList.add("hidden");

    document.getElementById("votingScreen")
    .classList.add("hidden");

    document.getElementById("cardScreen")
    .
