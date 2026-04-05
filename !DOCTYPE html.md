<!DOCTYPE html>  
<html>  
<head>  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<style>  
body {  
  background: #0f172a;  
  color: white;  
  text-align: center;  
  font-family: Arial;  
}  
  
.dealer {  
  position: relative;  
  width: 260px;  
  margin: auto;  
}  
  
video, .body {  
  width: 100%;  
  border-radius: 10px;  
}  
  
.head {  
  position: absolute;  
  top: 35px;  
  left: 75px;  
  width: 100px;  
  height: 100px;  
  border-radius: 50%;  
  object-fit: cover;  
  border: 2px solid white;  
}  
  
.cards {  
  margin-top: 20px;  
}  
  
.card {  
  display: inline-block;  
  width: 50px;  
  height: 70px;  
  background: white;  
  color: black;  
  margin: 5px;  
  line-height: 70px;  
  font-weight: bold;  
  border-radius: 5px;  
  transform: translateY(-100px);  
  opacity: 0;  
  transition: all 0.5s ease;  
}  
  
.card.show {  
  transform: translateY(0);  
  opacity: 1;  
}  
  
button {  
  padding: 10px;  
  margin: 10px;  
  font-size: 16px;  
}  
</style>  
</head>  
<body>  
  
<h2>Dealer Card Game</h2>  
  
<div class="dealer">  
  <!-- Replace with your own video later -->  
  <img class="body" src="https://via.placeholder.com/260x360">  
  <img id="head" class="head" src="https://via.placeholder.com/100">  
</div>  
  
<br>  
<input type="file" id="upload" accept="image/*">  
  
<div class="cards" id="cards"></div>  
  
<h3 id="result"></h3>  
  
<button onclick="dealCards()">Deal Cards</button>  
  
<script>  
const suits = ["♠","♥","♦","♣"];  
  
function getRandomCard() {  
  return {  
    value: Math.floor(Math.random() * 13) + 1,  
    suit: suits[Math.floor(Math.random() * suits.length)]  
  };  
}  
  
function dealCards() {  
  const container = document.getElementById("cards");  
  const result = document.getElementById("result");  
  container.innerHTML = "";  
  result.innerText = "";  
  
  let playerTotal = 0;  
  let dealerTotal = 0;  
  
  for (let i = 0; i < 3; i++) {  
    const playerCard = getRandomCard();  
    const dealerCard = getRandomCard();  
  
    playerTotal += playerCard.value;  
    dealerTotal += dealerCard.value;  
  
    createCard(playerCard, i * 300);  
  }  
  
  setTimeout(() => {  
    if (playerTotal > dealerTotal) {  
      result.innerText = "You win!";  
    } else if (playerTotal < dealerTotal) {  
      result.innerText = "Dealer wins!";  
    } else {  
      result.innerText = "Draw!";  
    }  
  }, 1200);  
}  
  
function createCard(card, delay) {  
  const div = document.createElement("div");  
  div.className = "card";  
  div.innerText = card.value + card.suit;  
  
  document.getElementById("cards").appendChild(div);  
  
  setTimeout(() => {  
    div.classList.add("show");  
  }, delay);  
}  
  
// Upload custom head  
document.getElementById("upload").addEventListener("change", function(event) {  
  const file = event.target.files[0];  
  if (file) {  
    const url = URL.createObjectURL(file);  
    document.getElementById("head").src = url;  
  }  
});  
</script>  
  
</body>  
</html>  
  
  
