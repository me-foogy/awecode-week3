<script setup lang="ts">
    const emit = defineEmits<{
        (e: 'closeButtonClick', value: boolean):void;
    }>();
    const buttonClick = ():void =>{
        emit('closeButtonClick', false);
    }
</script>

<template>
    <div class="initial-component-background">
        <div class="initial-component-content">
            <h2>Welcome to the Reaction Checker Game</h2>
            <p>Instructions</p>
            <ul>
                <li>Click Start to begin the game.</li>
                <li>Press the button as quickly as possible when it turns blue.</li>
                <li>Your reaction time will be measured and displayed.</li>
            </ul>
            <button class="default-btn-style" @click="buttonClick">Close</button>
        </div>
    </div>
</template>

<style scoped>
    .initial-component-background{
        position: fixed;
        width: 100vw;
        height: 100vh;
        background-color: rgba(0,0,0,0.6);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 9999;
    }
    .initial-component-content{
        background-color: white;
        padding: 2rem;
        border-radius: 1rem;
        text-align: center;
        box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }
    .initial-component-content ul{
        padding: 1rem 0;
        list-style-type: none;
        text-align: start;
    }
</style>