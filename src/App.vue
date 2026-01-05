<script setup lang="ts">
    import {ref} from 'vue';
    import GameComponent from './components/GameComponent.vue';
    import ShowResult from './components/ShowResult.vue';
import InitialInstructions from './components/initialInstructions.vue';

    const gameState = ref<'idle'|'start'|'waiting'|'end'>('idle');
    let timer:number = 0 ;
    const btnState = ref<boolean>(false);
    const showResult = ref<boolean>(false);
    const showInstructions = ref<boolean>(true); 

    function startGame():void {
      btnState.value = true;
      gameState.value = 'start';
    }

    function restartGame(){
      gameState.value='idle';
      timer = 0;
      btnState.value=false;
      showResult.value = false;
    }

    const changeGameState = (state: 'idle'|'start'|'waiting'|'end'):void=>{
      gameState.value=state;
      console.log(gameState.value);
    }

    const handleSendTimer = (timerValue: number): void =>{
      if(typeof(timerValue)=='number')
      timer=timerValue;
      //display result
      showResult.value=true;
    }

    const handleCloseClick = (buttonState: boolean):void=>{
      showInstructions.value = buttonState
    }
</script>

<template>
  <div class="center-everything">
    <InitialInstructions v-if="showInstructions" @closeButtonClick="handleCloseClick"/>
    <h1 class="title">Reaction checker Game</h1>
    <p class="title-description">This is a game in which the reaction time of the player is checked</p>
    <button v-show="gameState!=='end'" class="default-btn-style start-game" :disabled="btnState" @click="startGame">START</button>
    <button v-show="gameState==='end'" class="default-btn-style restart-game" @click="restartGame">PLAY GAIN</button>
    <GameComponent v-if="gameState!=='idle'" @sendTimer="handleSendTimer" @changeGameState="changeGameState"/>
    <ShowResult v-if="showResult" :timer="timer" @changeGameState="changeGameState"/>
  </div>
</template>

<style scoped>
  .title{
    margin-top: 4rem;
  }

  .title-description{
    margin-bottom: 2rem;
  }

  .center-everything{
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    background-image: url(../public/background.jpg);
    background-repeat: no-repeat;
    background-size: cover;
  }

  .start-game:disabled{
    background-color: #EB455F !important;
    color: white;
    cursor:default;
  }
</style>
