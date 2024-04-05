---
toc: false
comments: false
layout: default
---
<html lang="en">
<head>
    <!-- Meta tags for character set and viewport -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Title of the webpage -->
    <title>Baccarat</title>
    <!-- Styles for the webpage -->
    <style>
        body {
            width: 100%;
            height: 100%;
            margin: 0em 0%;
            background-color: #8ec1da;
            background-image: url("https://static.vecteezy.com/system/resources/previews/016/124/733/non_2x/poker-and-casino-playing-card-black-background-vector.jpg");
            background-position: center bottom;
        }
        .playercardsbox, .Bankercardsbox {
            position: fixed;
            top: 70%;
            transform: translate(-50%, -50%);
            background-color: rgba(38, 152, 255, 0.3) !important;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
            font-size: 30px;
            font-family: Verdana, sans-serif;
            overflow-y: auto; /*Enable vertical scroll if needed */
        }
        .playercardsbox::before, .Bankercardsbox::before {  
            transform: scaleX(0);
            transform-origin: bottom right;
        }
        .playercardsbox:hover::before, .Bankercardsbox:hover::before {
            transform: scaleX(1);
            transform-origin: bottom left;
        }
        .home-button {
            position: fixed;
            top: 20px;
            left: 20px;
            z-index: 9999;
        }
        .home-button a {
            text-decoration: none;
            color: white;
            background-color: #007bff;
            padding: 10px 20px;
            border-radius: 5px;
        }
        .home-button a:hover {
            background-color: #0056b3;
        }
        .playercardsbox::before, .Bankercardsbox::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; right: 0; bottom: 0; left: 0;
            inset: 0 0 0 0;
            background-color: rgba(128, 128, 128, 0.5);
            z-index: -1;
            transition: transform .3s ease;
        }
        @media (orientation: landscape) {
        body {
            grid-auto-flow: column;
        }
        }
        .playercardsbox {
            left: 30%;
            max-height: 100%; 
        }
        .Bankercardsbox {
            left: 70%;
            max-height: 100%;
        }
        .result {
            position: fixed;
            top: 34%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 150px;
            font-family: Verdana, sans-serif;
            color: red;
            display: none;
        }
        .betplayer, .betbanker, .bettie, .tempresetbutton {
            position: fixed;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(38, 152, 255, 0.5);
            border: none;
            width: 10%;
            height: 10%;
            border-radius: 10px;
            font-size: 30px;
            font-family: Verdana, sans-serif;
        }
        .betplayer:hover, .betbanker:hover, .bettie:hover, .tempresetbutton:hover {
            background-color: rgba(38, 152, 255, 0.3) !important;
        }
        .betbanker {
            top: 62.5%;
        }
        .betplayer {
            top: 75%;
        }
        .bettie { 
            top: 50%;
            display: block
        }
        .tempresetbutton {
            top: 90%
        }
        .betprompt {
            position: fixed;
            top: 26%;
            left: 50%;
            font-size: 80px;
            transform: translate(-50%, -50%);
        }
        .money {
            position: fixed;
            top: 20%;
            left: 80%;
            font-size: 80px;
            transform: translate(-50%, -50%);
            border: none;
            width: 10%;
            height: 10%;
            border-radius: 10px;
        }
        .moneyinside {
            font-size: 30px;
            font-family: Verdana, sans-serif;
        }
        .playersumbox, .Bankersumbox {
            position: fixed;
            top: 53%;
            transform: translate(-50%, -50%);
            background-color: rgba(128, 128, 128, 0.5);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
            font-size: 30px;
            font-family: Verdana, sans-serif;
            display: none;
        }
        .playersumbox {
            left: 30%;
        }
        .Bankersumbox {
            left: 70%;
        }
        .floating { 
            animation-name: floating;
            animation-duration: 3s;
            animation-iteration-count: infinite;
            animation-timing-function: ease-in-out;
            margin-left: 10px;
            margin-top: 5px;
            top: 10%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 60px;
            font-family: Andale Mono, monospace;
        }
        @keyframes floating {
            0% { transform: translate(0, 0px); }
            50% { transform: translate(0, 15px); }
            100% { transform: translate(0, -0px); }
        }
        .betinput {
            position: fixed;
            top: 38%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
</style>
</head>
<body>
<div class="floating">
    <!-- Title of the game -->
    <h1 class="floating">BACCARAT</h1>
</div>
<div class="playercardsbox" id="playercardsbox">
    <!-- Player's card box with placeholder text -->
    <p><strong>Player Cards:</strong></p>
</div>
<div class="Bankercardsbox" id="Bankercardsbox">
    <!-- Banker's card box with placeholder text -->
    <p><strong>Banker Cards:</strong></p>
</div>
<div class="result" id="result">Bust!</div>
<div class="playersumbox" id="playersumbox">
    <p><strong></strong></p>
</div>
<div class="Bankersumbox" id="Bankersumbox">
    <p><strong></strong></p>
</div>
<div>
    <!-- Buttons for player actions -->
    <button class="betplayer" id="choosebetplayer" onclick="choosebet('p')">PLAYER</button>
    <button class="betbanker" id="choosebetbanker" onclick="choosebet('b')">BANKER</button>
    <button class="bettie" id="choosebettie" onclick="choosebet('t')">TIE</button>
    <h1 class="betprompt" id="pickabet">PLACE YOUR BET</h1>
    <button class="tempresetbutton" onclick="resetGame()">RESET</button>
</div>
<div class="home-button">
    <a href="http://127.0.0.1:4100/ByteJam/2024/02/08/Main.html">Home</a>
</div>
<div>
    <input class="betinput" type="number" id="betvalue" placeholder="Bet Amount" onkeypress="checkEnter(event)">
</div>
<div class="money" id="moneydisplay">
    <p class="moneyinside" id="moneydisplayinside">asdf</p>
</div>
<script>
    // Game variables
    var cardcounter = 52;
    var playercardcounter = 0;
    var Bankercardcounter = 0;
    var picktie = false;
    var pickplayer = false;
    var pickbanker = false;
    var istie = false;
    var isplayer = false;
    var isbanker = false;
    var chosen = false;
    var lastplayercard;
    var lastbankercard;
    var playerbet = 0;
    var money = 200;
    function updatemoney() {
        document.getElementById("moneydisplayinside").innerHTML = money
    }
    updatemoney()
    function saveValue() {
        playerbet = document.getElementById("betvalue").value;
        document.getElementById("betvalue").value = "";
    }
    function checkEnter(event) {
        if (event.key === "Enter") {
            saveValue();
        }
    }
    // Function to generate a deck of cards
    function choosebet(bet) {
        if (chosen == false) {
            document.getElementById("pickabet").style.display = "none";
            if (bet == "p") {
                pickplayer = true;
                document.getElementById("choosebettie").style.display = "none";
                document.getElementById("choosebetbanker").style.display = "none";
            }
            else if (bet == "b") {
                pickbanker = true;
                document.getElementById("choosebettie").style.display = "none";
                document.getElementById("choosebetplayer").style.display = "none";
            }
            else if (bet == "t") {
                picktie = true;
                document.getElementById("choosebetbanker").style.display = "none";
                document.getElementById("choosebetplayer").style.display = "none";
            }
            saveValue()
            console.log(playerbet)
            money -= playerbet
            updatemoney()
            playercards();
            Bankercards();
            calculatePlayerScore();
            calculateBankerScore();
            chosen = true
            afterbet()
        }
    }
    function shuffleArray(array) {
        for (var i = array.length - 1; i > 0; i--) {
            var j = Math.floor(Math.random() * (i + 1));
            var temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
    }
    function generatecards() {
        var numbers = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"];
        var suits = ["♠︎", "♥︎", "♦︎", "♣︎"];
        var cards = [];
        for (let i = 0; i < numbers.length; i++) {
            for (let j = 0; j < suits.length; j++) {
                cards.push(numbers[i] + suits[j]);
            }
        }
        return cards;
    }
    // Initialize the deck
    var deck = generatecards();
    // Function to deal initial cards to the player
    function playercards() {
        // Generate random indices for two cards
        var num1 = Math.floor(Math.random()*cardcounter);
        var num2 = Math.floor(Math.random()*(cardcounter-1));
        var card1 = deck[num1];
        deck.splice(num1, 1);
        cardcounter -= 1;
        var card2 = deck[num2];
        deck.splice(num2, 1);
        cardcounter -= 1;
        // Display player's cards and calculate the score
        var card1Element = document.getElementById("playercardsbox");
        card1Element.innerHTML += card1 + "<br>";
        card1Element.innerHTML += card2 + "<br>";
        playercardcounter = 2;
        // calculatePlayerScore();
    }
    // Function to deal initial cards to the Banker
    function Bankercards() {
        // Generate random indices for two cards
        var num1 = Math.floor(Math.random()*cardcounter);
        var num2 = Math.floor(Math.random()*(cardcounter-1));
        // Convert cards to binary and remove them from the deck
        var Bankercard1 = deck[num1];
        deck.splice(num1, 1);
        cardcounter -= 1;
        var Bankercard2 = deck[num2];
        deck.splice(num2, 1);
        cardcounter -= 1;
        // Display Banker's cards and calculate the score
        var Bankercard1Element = document.getElementById("Bankercardsbox");
        Bankercard1Element.innerHTML += Bankercard1 + "<br>";
        Bankercard1Element.innerHTML += Bankercard2 + "<br>";
        Bankercardcounter = 2;
        // calculateBankerScore();
    }
    // Function to calculate the player's score
    function calculatePlayerScore() {
        // Get player's cards from the HTML content
        var playerCards = document.getElementById("playercardsbox").textContent;
        // Extract card values from the text content
        var cardValues = playerCards.match(/\d+|A|J|Q|K/g);
        var sum = 0;
        if (cardValues) {
            // Calculate the sum of card values
            for (var i = 0; i < cardValues.length; i++) {
                var value = 0;
                if (cardValues[i] === "A") {
                    value = 1;
                } else if (["J", "Q", "K"].includes(cardValues[i])) {
                    value = 0;
                } else {
                    value = parseInt(cardValues[i]);
                }
                sum += value;
            }
        }
        // Return the calculated score
        //console.log(sum)
        sum %= 10
        //console.log(sum)
        return sum;
    }
    // Function to calculate the Banker's score
    function calculateBankerScore() {
        // Get Banker's cards from the HTML content
        var BankerCards = document.getElementById("Bankercardsbox").textContent;
        // Extract card values from the text content
        var cardValues = BankerCards.match(/\d+|A|J|Q|K/g);
        var sum = 0;
        if (cardValues) {
            // Calculate the sum of card values
            for (var i = 0; i < cardValues.length; i++) {
                var value = 0;
                if (cardValues[i] === "A") {
                    value = 1;
                } else if (["J", "Q", "K", "10"].includes(cardValues[i])) {
                    value = 0;
                } else {
                    value = parseInt(cardValues[i]);
                }
                sum += value;
            }
        }
        // Return the calculated score
        // console.log(sum)
        sum %= 10
        // console.log(sum)
        return sum;
    }
    // Function to draw a card for the player
    function getplayercard() {
        // Generate a random card index
        var tempnum = Math.floor(Math.random() * cardcounter);
        var temp = deck[tempnum];
        var card = temp;
        lastplayercard = temp;
        lastplayercard = lastplayercard.substring(0, lastplayercard.length - 2);
        deck.splice(tempnum, 1);
        cardcounter -= 1;
        // Display the drawn card
        var cardElement = document.getElementById("playercardsbox");
        cardElement.innerHTML += card + "<br>";
        playercardcounter += 1;
        // Calculate the player's score and handle bust
        var playerScore = calculatePlayerScore();
    }
    // Function to handle player's stand action
    function stand() {
        // Check if the player is not busted
        if (!playerBusted) {
            // Check if the Banker has a higher score and compare scores
            if (calculateBankerScore() > calculatePlayerScore()) {
                compareScores();
            }
            // Draw cards for the Banker until reaching a score of 17 or higher
            while (calculateBankerScore() < 17) {
                getBankercard();
            }
        }
        // Compare scores after the Banker's final draw
        compareScores();
    }
    // Function to draw a card for the Banker
    function getBankercard() {
        // Generate a random card index
        var tempnum = Math.floor(Math.random() * cardcounter);
        var card = deck[tempnum];
        lastbankercard = card;
        lastbankercard = lastbankercard.slice(0, -2);
        // Remove the drawn card from the deck
        deck.splice(tempnum, 1);
        cardcounter -= 1;
        // Display the drawn card for the Banker
        var cardElement = document.getElementById("Bankercardsbox");
        cardElement.innerHTML += card + "<br>";
        // Calculate the Banker's score
        calculateBankerScore();
    }
    // Function to reset the game
    function resetGame() {
        // Reset game variables and display
        cardcounter = 52;
        playercardcounter = 0;
        Bankercardcounter = 0;
        document.getElementById("playercardsbox").innerHTML = "<p><strong>Player Cards:</strong></p>";
        document.getElementById("Bankercardsbox").innerHTML = "<p><strong>Banker Cards:</strong></p>";
        //document.getElementById("playerscore").innerText = "";
        //document.getElementById("Bankerscore").innerText = "";
        document.getElementById("result").style.display = "none";
        document.getElementById("playersumbox").style.display = "none";
        document.getElementById("Bankersumbox").style.display = "none";
        document.getElementById("choosebetplayer").style.display = "block";
        document.getElementById("choosebetbanker").style.display = "block";
        document.getElementById("choosebettie").style.display = "block";
        document.getElementById("pickabet").style.display = "block";
        picktie = false;
        pickplayer = false;
        pickbanker = false;
        istie = false;
        isplayer = false;
        isbanker = false;
        chosen = false
        deck = generatecards();
    }
    function defaultcheck(player, banker) {
    // Function to handle default comparison
    if (ps > bs) {
        console.log("player win")
        if (pickplayer) {
            money += playerbet*2 
            updatemoney()
        }
        }
    else if (ps < bs) {
        console.log("banker win")
        if (pickbanker) {
            money += parseInt(playerbet)
            money += parseInt(Math.floor(playerbet*0.95))
            console.log(Math.floor(playerbet*0.95))
            updatemoney()
        }
    }
    else if (ps == bs) {
        console.log("tie", ps)
        if (picktie) {
            money += playerbet*10
            updatemoney()
        }
    }
    }
    function afterbet() {
        // Function to handle game logic
        ps = calculatePlayerScore()
        bs = calculateBankerScore()
        console.log(ps, bs)
        if (ps == 8 || ps == 9 || bs == 8 || bs == 9) {
            // One or both players has a natural win
            if (ps == bs) {
                defaultcheck(ps, bs)
            }
            else if (ps == 9 && bs == 8 || (ps == 9 || ps == 8 && bs != 8 && bs != 9)) {
                defaultcheck(ps, bs)
            }
            else if (ps == 8 && bs == 9 || (bs == 9 || bs == 8 && ps != 8 && ps != 9)) {
                defaultcheck(ps, bs)
            }
            }
        else if (ps <= 5) {
            //Player draws a new card
            getplayercard()
            ps = calculatePlayerScore()
            if (ps >= 8) {
                // Natural win for player
                defaultcheck(ps, bs)
            }
            // Check if the banker should draw a third card based on player's third card and banker's current score
            else if (
                (['9', '10', 'J', 'Q', 'K', 'A'].includes(lastplayercard) && bs <= 3) ||
                (lastplayercard == '8' && bs <= 2) ||
                ((lastplayercard == '6' || lastplayercard == '7') && bs <= 6) ||
                ((lastplayercard == '5' || lastplayercard == '4') && (bs == 5 || bs == 6)) ||
                ((lastplayercard == '2' || lastplayercard == '3') && bs <= 4)) {
                // Banker draws a new card
                getBankercard();
                bs = calculateBankerScore();
                console.log(ps, bs)
                // Check game result after banker draws
                defaultcheck(ps, bs);
            } 
            else if (
                (['9', '10', 'J', 'Q', 'K', 'A'].includes(lastplayercard) && bs >= 4 && bs <= 7) ||
                (lastplayercard == '8' && bs <= 7 && bs >= 3) ||
                ((lastplayercard == '6' || lastplayercard == '7') && bs == 7) ||
                ((lastplayercard == '5' || lastplayercard == '4') && (bs == 6 || bs == 7)) ||
                ((lastplayercard == '2' || lastplayercard == '3') && bs <= 7 && bs >= 5)) {
                // Banker doesn't draw a new card
                // Check game result without banker drawing
                defaultcheck(ps, bs);
            }
            }
        else if (ps == '7' || ps == '6') {
            if (bs <= 5) {
                getBankercard();
                bs = calculateBankerScore()
                defaultcheck(ps, bs)
            }
            else {
                defaultcheck(ps, bs)
            }
        }
        }
// Function calls to initialize the game


</script>
</body>