<script setup>
import { ref } from 'vue';
const imgpaperLeft = ref(new URL('./assets/mini.png', import.meta.url).href);
const imgpaperRight = ref(new URL('./assets/mini.png', import.meta.url).href);
const scoreTeamA = ref(0);
const scoreTeamB = ref(0);
const gameResult = ref('-------');

// Create an array of options
const options = ['Rock', 'Paper', 'Scissors', 'Lovely'];

function getRandomOption() {
  const randomIndex = Math.floor(Math.random() * options.length);
  return options[randomIndex];
}

function startGame() {
  const rd1 = getRandomOption();
  const rd2 = getRandomOption();

  // Map the options to image URLs
  const imageMapping = {
    'Rock': 'rock.png',
    'Paper': 'PaperR.png',
    'Scissors': 'scisorr.png',
    'Lovely': 'mini.png',
  };

  imgpaperLeft.value = new URL(`./assets/${imageMapping[rd1]}`, import.meta.url).href;
  imgpaperRight.value = new URL(`./assets/${imageMapping[rd2]}`, import.meta.url).href;

  // Determine the winner and update the score and game result
  if (rd1 === rd2) {
    // It's a tie
    gameResult.value = 'Tie!';
  } else if(rd1 === 'Lovely'){
    gameResult.value =  'Team A wins!';
    scoreTeamA.value += 1;
  }else if(rd2 === 'Lovely'){
    gameResult.value = 'Team B wins!';
    scoreTeamB.value += 1;
  } else if ((rd1 === 'Paper' && rd2 === 'Rock') || (rd1 === 'Scissors' && rd2 === 'Paper') || (rd1 === 'Rock' && rd2 === 'Scissors')) {
    gameResult.value = 'Team A wins!';
    scoreTeamA.value += 1;
  } else {
    gameResult.value = 'Team B wins!';
    scoreTeamB.value += 1; 
  }
}

function resetGame() {
  imgpaperLeft.value = new URL(`./assets/mini.png`, import.meta.url).href;
  imgpaperRight.value = new URL(`./assets/mini.png`, import.meta.url).href;
  scoreTeamA.value = 0;
  scoreTeamB.value = 0;
  gameResult.value = '-------';
}
</script>

<template>
  <div class="image-container">
    <div class="image-frame">
      <h2 class="centered-text">Rock-Paper-Scissors-Love</h2>
      
      <h1 class="centered-text">Score: {{ scoreTeamA }} - {{ scoreTeamB }}</h1>
      <p class="centered-text result">{{ gameResult }}</p>
      <div class="game-zone">
        <div class="team-image">
          <p class="team-name">Team A</p>
          <img class="left-image" :src="imgpaperLeft" alt="Image Left">
        </div>
        <div class="team-image">
          <p class="team-name">Team B</p>
          <img class="right-image" :src="imgpaperRight" alt="Image Right">
        </div>
      </div>
      <div class="button-container">
        <button class="play-button" @click="startGame">Play Game</button>
        <button class="reset-button" @click="resetGame">Reset</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

.game-zone {
  
  width: 100%; /* Extend the game zone width to 80% */
  margin: 0 auto; /* Center the game zone horizontally */
  display: flex; /* Display the team images in a flex container */
  justify-content: space-between; /* Space between the team images */
}

.team-image {
  flex: 1; /* Equal width for both team images */
  text-align: center;
}
.image-container {
  text-align: center;
}

.image-frame {
  display: inline-block;
  align-items: center;
  background-color: rgb(255, 255, 255);
  padding: 100px; 
  border: 25px solid #E0C7EE;
  border-radius: 100px;
}

.centered-text {
  text-align: center;
}


.team-name {
  font-weight: bold;
  font-size: 20px;
}

.team-image {
  text-align: center;
}

.team-image img {
  width: 200px;
  height: 200px;
  background-color: lightblue;
  margin-top: 20px;
}

.result {
  font-size: 24px;
  font-weight: bold;
  color: #FF5733; /* Change the color to your preference */
  margin-bottom: 20px;
}

.left-image {
  float: left;
  margin-right: 100px;
  width: 300px;
  height: 300px;
  background-color: lightblue;
  margin-top: 20px;
}

.right-image {
  float: right;
  margin-left: 100px;
  width: 300px;
  height: 300px;
  background-color: lightgreen;
  clear: right;
  margin-top: 20px;
}
</style>
