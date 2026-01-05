<script setup lang="ts">
    import {ref, watchEffect} from 'vue';

    const btnMessage = ref<string>('Press This button as fast as possible when button color changes to blue');
    const btnState = ref<boolean>(true);
    let timer:number | null = null;

    const buttonTimer = ():void => {
        let timer = 3000+Math.floor(Math.random()*6)*1000 //genrate number from 0 to 5 and convert to seconds [starts from 3 to 8]
        setTimeout(()=>{
            btnState.value=false;
            timerFunction();
        }, timer);
    }
    watchEffect(buttonTimer);
    function timerFunction():void{
        if(timer){
            console.log('timer is being executed for the second time');
            timer= Date.now()-timer;
            emit('sendTimer', timer);
            emit('changeGameState', 'end')
        }else{
            console.log('timer is being executed for the first time');
            timer= Date.now();
            console.log(timer);
            emit('changeGameState', 'waiting');
        }
    }

    const emit = defineEmits(['sendTimer','changeGameState']);

</script>

<template>
    <button class="reaction-test-btn" :disabled="btnState" @click="timerFunction">
        {{btnMessage}}
    </button>
</template>

<style scoped>
    .reaction-test-btn{
        margin-top: 2rem;
        width: 30rem;
        height: 12rem;
        border-radius: 2rem;
        cursor: pointer;
        background-color: #2B3467;
        padding: 2rem;
        color: white;
    }
    .reaction-test-btn:disabled{
        background-color: #BAD7E9;
        color: black;
    }
</style>