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
    <title>Blackjack</title>
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
        .playercardsbox, .dealercardsbox {
            position: fixed;
            top: 77%;
            transform: translate(-50%, -50%);
            background-color: rgba(38, 152, 255, 0.3) !important;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
            font-size: 30px;
            font-family: Verdana, sans-serif;
            overflow-y: auto; /*Enable vertical scroll if needed */
        }
        .playercardsbox::before, .dealercardsbox::before {  
            transform: scaleX(0);
            transform-origin: bottom right;
        }
        .playercardsbox:hover::before, .dealercardsbox:hover::before {
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
        .playercardsbox::before, .dealercardsbox::before {
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
            max-height: 100%; /* Allow it to grow to the full height of the viewport*/
        }
        .dealercardsbox {
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
        .hitbutton, .standbutton, .resetbutton {
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
        .hitbutton:hover, .standbutton:hover, .resetbutton:hover {
            background-color: rgba(38, 152, 255, 0.3) !important;
        }
        .standbutton {
            top: 72%
        }
        .hitbutton {
            top: 60%
        }
        .resetbutton {
            top: 84%;
            display: block
        }
        .playersumbox, .dealersumbox {
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
        .dealersumbox {
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
            left: 60%;
            transform: translate(-50%, -50%);
            font-size: 60px;
            font-family: Monochrome;
        }
        @keyframes floating {
            0% { transform: translate(0, 0px); }
            50% { transform: translate(0, 15px); }
            100% { transform: translate(0, -0px); } 
        }
    </style>
</head>
<body>
<div class="floating">
    <!-- Title of the game -->
    <h1 class="floating">Blackjack</h1>
</div>
<div class="playercardsbox" id="playercardsbox">
    <!-- Player's card box with placeholder text -->
    <p><strong>Player Cards:</strong></p>
</div>
<div class="dealercardsbox" id="dealercardsbox">
    <!-- Dealer's card box with placeholder text -->
    <p><strong>Dealer Cards:</strong></p>
</div>
<div class="result" id="result">Bust!</div>
<div class="playersumbox" id="playersumbox">
    <p><strong></strong></p>
</div>
<div class="dealersumbox" id="dealersumbox">
    <p><strong></strong></p>
</div>
<div>
    <!-- Buttons for player actions -->
    <button class="hitbutton" onclick="getplayercard()">Hit</button>
    <button class="standbutton" onclick="stand()">Stand</button>
    <button class="resetbutton" onclick="resetGame()">Reset</button>
</div>
    <div class="home-button">
        <a href="http://127.0.0.1:4100/teacher_portfolio/">Home</a>
    </div>
<script>
    // Game variables
    var cardcounter = 52;
    var playercardcounter = 0;
    var dealercardcounter = 0;
    var playerBusted = false;
    // Function to generate a deck of cards
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
        var num1 = Math.floor(Math.random()*52);
        var num2 = Math.floor(Math.random()*51);
        // Convert cards to binary and remove them from the deck
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
        calculatePlayerScore();
    }
    // Function to deal initial cards to the dealer
    function dealercards() {
        // Generate random indices for two cards
        var num1 = Math.floor(Math.random()*50);
        var num2 = Math.floor(Math.random()*49);
        // Convert cards to binary and remove them from the deck
        var dealercard1 = deck[num1];
        deck.splice(num1, 1);
        cardcounter -= 1;
        var dealercard2 = deck[num2];
        deck.splice(num2, 1);
        cardcounter -= 1;
        // Display dealer's cards and calculate the score
        var dealercard1Element = document.getElementById("dealercardsbox");
        dealercard1Element.innerHTML += dealercard1 + "<br>";
        dealercard1Element.innerHTML += dealercard2 + "<br>";
        dealercardcounter = 2;
        calculateDealerScore();
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
                // Assign values to cards (considering Ace as 11)
                if (cardValues[i] === "A") {
                    value = 11;
                } else if (["J", "Q", "K"].includes(cardValues[i])) {
                    value = 10;
                } else {
                    value = parseInt(cardValues[i]);
                }
                sum += value;
            }
        }
        // Adjust for Ace if needed
        for (var i = 0; i < cardValues.length; i++) {
            if (cardValues[i] === "A" && sum > 21) {
                sum -= 10;
            }
        }
        // Return the calculated score
        return sum;
    }
    // Function to calculate the dealer's score
    function calculateDealerScore() {
        // Get dealer's cards from the HTML content
        var dealerCards = document.getElementById("dealercardsbox").textContent;
        // Extract card values from the text content
        var cardValues = dealerCards.match(/\d+|A|J|Q|K/g);
        var sum = 0;
        if (cardValues) {
            // Calculate the sum of card values
            for (var i = 0; i < cardValues.length; i++) {
                var value = 0;
                // Assign values to cards (considering Ace as 11)
                if (cardValues[i] === "A") {
                    value = 11;
                } else if (["J", "Q", "K", "10"].includes(cardValues[i])) {
                    value = 10;
                } else {
                    value = parseInt(cardValues[i]);
                }
                sum += value;
            }
        }
        // Adjust for Ace if needed
        for (var i = 0; i < cardValues.length; i++) {
            if (cardValues[i] === "A" && sum > 21) {
                sum -= 10;
            }
        }
        // Return the calculated score
        return sum;
    }
    // Function to draw a card for the player
    function getplayercard() {
        // Check if the player is not busted
        if (!playerBusted) {
            // Generate a random card index
            var tempnum = Math.floor(Math.random() * cardcounter);
            var temp = deck[tempnum];
            // Convert the card to binary and update the deck
            var card = temp;
            deck.splice(tempnum, 1);
            cardcounter -= 1;
            // Display the drawn card
            var cardElement = document.getElementById("playercardsbox");
            cardElement.innerHTML += card + "<br>";
            playercardcounter += 1;
            // Calculate the player's score and handle bust
            var playerScore = calculatePlayerScore();
            if (playerScore > 21) {
                handlePlayerBust();
            }
        }
    }
    // Function to handle the player bust
    function handlePlayerBust() {
        playerBusted = true;
        document.getElementById("result").innerText = "Bust!";
        document.getElementById("result").style.display = "block";
        // Call the displaySums function
        displaySums();
    }
    // Function to handle player's stand action
    function stand() {
        // Check if the player is not busted
        if (!playerBusted) {
            // Check if the dealer has a higher score and compare scores
            if (calculateDealerScore() > calculatePlayerScore()) {
                compareScores();
            }
            // Draw cards for the dealer until reaching a score of 17 or higher
            while (calculateDealerScore() < 17) {
                getdealercard();
            }
        }
        // Compare scores after the dealer's final draw
        compareScores();
    }
    // Function to draw a card for the dealer
    function getdealercard() {
        // Generate a random card index
        var tempnum = Math.floor(Math.random() * cardcounter);
        var card = deck[tempnum];
        // Remove the drawn card from the deck
        deck.splice(tempnum, 1);
        cardcounter -= 1;
        // Display the drawn card for the dealer
        var cardElement = document.getElementById("dealercardsbox");
        cardElement.innerHTML += card + "<br>";
        // Calculate the dealer's score
        calculateDealerScore();
    }
    // Function to compare the final scores and determine the winner
    function compareScores() {
        var playerScore = calculatePlayerScore();
        var dealerScore = calculateDealerScore();
        // Check for bust, win, tie, or loss
        if (playerScore > 21) {
            handlePlayerBust();
        } else {
            if (dealerScore > 21 || playerScore > dealerScore) {
                document.getElementById("result").innerText = "You Win!";
            } else if (playerScore === dealerScore) {
                document.getElementById("result").innerText = "It's a Tie!";
            } else {
                document.getElementById("result").innerText = "You Lose!";
            }
            document.getElementById("result").style.display = "block";
            // Display the sums
            displaySums();
        }
    }
    // Function to reset the game
    function resetGame() {
        // Reset game variables and display
        cardcounter = 52;
        playercardcounter = 0;
        dealercardcounter = 0;
        document.getElementById("playercardsbox").innerHTML = "<p><strong>Player Cards:</strong></p>";
        document.getElementById("dealercardsbox").innerHTML = "<p><strong>Dealer Cards:</strong></p>";
        //document.getElementById("playerscore").innerText = "";
        //document.getElementById("dealerscore").innerText = "";
        document.getElementById("result").style.display = "none";
        document.getElementById("playersumbox").style.display = "none";
        document.getElementById("dealersumbox").style.display = "none";
        playerBusted = false;
        // Wait for confetti animation to finish before removing confetti elements
    setTimeout(() => {
        // Remove confetti elements
        var existingConfetti = document.getElementsByClassName("confetti");
        while (existingConfetti.length > 0) {
            existingConfetti[0].parentNode.removeChild(existingConfetti[0]);
        }
    }, 4500); // Adjust the timeout value based on your confetti animation duration
        // Regenerate the deck and deal initial cards
        deck = generatecards();
        playercards();
        dealercards();
    }
    function calculateSum(cardsboxId) {
        var cardValues = document.getElementById(cardsboxId).textContent.match(/\d+|A|J|Q|K/g);
        var sum = 0;
        if (cardValues) {
            for (var i = 0; i < cardValues.length; i++) {
                var value = (cardValues[i] === "A") ? 11 : (["J", "Q", "K", "10"].includes(cardValues[i]) ? 10 : parseInt(cardValues[i]));
                sum += value
            }
        }
        // Convert the sum to binary
        return sum
    }
    function displaySums() {
        // Display the sum boxes
        document.getElementById("playersumbox").style.display = "block";
        document.getElementById("dealersumbox").style.display = "block";
        // Calculate and display player sum in binary
        var playerSum = calculateSum("playercardsbox");
        var playerSumdecimal = playerSum
        document.getElementById("playersumbox").innerText = "Player Sum: " + playerSum + " (" + playerSumdecimal + ")";
        // Calculate and display dealer sum in binary
        var dealerSum = calculateSum("dealercardsbox");
        var dealerSumdecimal = dealerSum
        document.getElementById("dealersumbox").innerText = "Dealer Sum: " + dealerSum + " (" + dealerSumdecimal + ")";
    }
// Function calls to initialize the game
playercards();
dealercards();
calculatePlayerScore();
calculateDealerScore();

</script>
</body>