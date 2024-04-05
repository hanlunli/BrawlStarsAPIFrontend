---
toc: false
comments: false
layout: default
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Poker</title>
    <style>
        BODY {
            background-image: url("https://static.vecteezy.com/system/resources/previews/016/124/733/non_2x/poker-and-casino-playing-card-black-background-vector.jpg");
            padding:20px;
            color:#DDDDDD;
            font-family:verdana;
            }
        #board, #playerCards, #aiCards {
            display: block;
            clear: both;
            width:100%;
            min-height: 240px;
            }
        .card {
            box-sizing: border-box;  
            width: 150px;
            height: 214px;
            margin: 10px;
            float: left;  
            background-color: white;
            background-image: url('./deckofcards1.png');
            background-position-x: 0px;
            background-position-y: center;
            background-repeat: none;
            background-position: middle center;  
            border: 1px #555555 solid;
            border-radius: 10px;
            -webkit-box-shadow: 2px 2px 3px 0px #000000; 
            box-shadow: 2px 2px 3px 0px #000000; 
            }
        HR {
            margin-top:12px;
            display: block;
            width:100%;
            }
        BUTTON {
            cursor: pointer;
            width:500px;
            height:40px;
            text-align:center;
            margin:20px;
            border-radius: 5px;
            }
    </style>
</head>
<body>
    Board:<div id="board" style="display: block;">
    <div id="card1"></div>
    <div id="card2"></div>
    <div id="card3"></div>
    <div id="card4"></div>
    <div id="card5"></div>
    </div>
    <hr/>
    Player's cards:
    <div id="playerCards">
    <div id="playerCard1"></div>
    <div id="playerCard2"></div>
    <div>
    <button onclick="javascript: nextStep(this);">Reveal first 3 cards</button>
    </div>
    </div> 
    <div id="aiCards">
    <div id="aiCard1"></div>
    <div id="aiCard2"></div>
    </div>
<script>
    class Deck {
        constructor() {
        this.deck = [];
        this.reset();
        this.shuffle();
        }
        reset() {
            this.deck = [];
            const suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades'];
            const values = ['Ace', 2, 3, 4, 5, 6, 7, 8, 9, 10, 'Jack', 'Queen', 'King'];
            for (let suit in suits) {
            for (let value in values) {
                this.deck.push(values[value] + " of " + suits[suit]);
            }
            }
        }
        shuffle() {
            let numberOfCards = this.deck.length;  
            for (var i=0; i<numberOfCards; i++) {
            let j = Math.floor(Math.random() * numberOfCards);
            let tmp = this.deck[i];
            this.deck[i] = this.deck[j];
            this.deck[j] = tmp;
            }
        }
        deal(){
            return this.deck.pop();
        }
        isEmpty() {
            return (this.deck.length==0);
        }
        length() {
            return this.deck.length;
        }
    }
class Card {
    constructor(card) {
        this.card = card;
        const cardValues = {"Ace of Hearts":1, "2 of Hearts":2, "3 of Hearts":3, "4 of Hearts":4, "5 of Hearts":5, "6 of Hearts":6, "7 of Hearts":7, "8 of Hearts":8, "9 of Hearts":9, "10 of Hearts":10, "Jack of Hearts":11, "Queen of Hearts":12, "King of Hearts":13, "Ace of Diamonds":1, "2 of Diamonds":2, "3 of Diamonds":3, "4 of Diamonds":4, "5 of Diamonds":5, "6 of Diamonds":6, "7 of Diamonds":7, "8 of Diamonds":8, "9 of Diamonds":9, "10 of Diamonds":10, "Jack of Diamonds":11, "Queen of Diamonds":12, "King of Diamonds":13, "Ace of Clubs":1, "2 of Clubs":2, "3 of Clubs":3, "4 of Clubs":4, "5 of Clubs":5, "6 of Clubs":6, "7 of Clubs":7, "8 of Clubs":8, "9 of Clubs":9, "10 of Clubs":10, "Jack of Clubs":11, "Queen of Clubs":12, "King of Clubs":13, "Ace of Spades":1, "2 of Spades":2, "3 of Spades":3, "4 of Spades":4, "5 of Spades":5, "6 of Spades":6, "7 of Spades":7, "8 of Spades":8, "9 of Spades":9, "10 of Spades":10, "Jack of Spades":11, "Queen of Spades":12, "King of Spades":13};
        this.value = cardValues[card];
        this.suit = card.substring(card.indexOf(" of ")+4);
        this.placeHolder = null;
        this.flipped = false;
        var suits = {'Hearts':0, 'Diamonds':13, 'Clubs':26, 'Spades':39 }
        this.position = suits[this.suit] + this.value; //Position in a sorted deck
    } //End of Constructor
    displayCard(placeHolder,flipped=true) {
        this.placeHolder = document.getElementById(placeHolder);
        this.placeHolder.classList.add("card");
        this.flipped=flipped;
        if (flipped) {
        this.placeHolder.style.backgroundPosition = -150*this.position + "px";
        } else {
        this.placeHolder.style.backgroundPosition = "0px";  
        }
    } // End of displayCard
    flip() {
        if (this.flipped) {
        this.placeHolder.style.backgroundPosition = "0px";
        this.flipped=false;
        } else {
        this.placeHolder.style.backgroundPosition = -150*this.position + "px";
        this.flipped=true;  
        }
    } //End of flip()
} //End of Card class
const deck = new Deck();
let card1,card2,card3,card4,card5,playerCard1,playerCard2,aiCard1,aiCard2;
function deal() {
    if (deck.length()<9) {
        deck.reset();
        deck.shuffle();
    }  
    card1 = new Card(deck.deal());
    card2 = new Card(deck.deal());
    card3 = new Card(deck.deal());
    card4 = new Card(deck.deal());
    card5 = new Card(deck.deal());
    playerCard1 = new Card(deck.deal());
    playerCard2 = new Card(deck.deal());
    aiCard1 = new Card(deck.deal());
    aiCard2 = new Card(deck.deal());
    card1.displayCard("card1",false);  
    card2.displayCard("card2",false);  
    card3.displayCard("card3",false);  
    card4.displayCard("card4",false);  
    card5.displayCard("card5",false);  
    playerCard1.displayCard("playerCard1",true);  
    playerCard2.displayCard("playerCard2",true); 
    aiCard1.displayCard("aiCard1",false);
    aiCard2.displayCard("aiCard2",false);
} //End of deal()
function nextStep(el) {
    if (!card1.flipped) {
        card1.flip();
        card2.flip();
        card3.flip();
        el.innerHTML="Reveal 4<sup>th</sup> card";
    } else if(!card4.flipped) {
        card4.flip();
        el.innerHTML="Reveal 5<sup>th</sup> card";
    } else if(!card5.flipped) {
        card5.flip();
        el.innerHTML="New Round";
        aiCard1.flip()
        aiCard2.flip()
    } else {
    deal();
    el.innerHTML="Reveal first 3 cards.";
    }
} //End of nextStep()
deal();
</script>
</body>
