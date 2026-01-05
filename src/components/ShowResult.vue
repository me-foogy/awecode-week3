<script setup lang="ts">
    import {computed} from 'vue';
        const props = defineProps<{
        timer: number
    }>();
    type resultCommentsKey = 'verySlow' | 'slow' | 'medium' | 'fast' | 'veryFast';
    const resultComments: Record<resultCommentsKey, String> = {
        verySlow: "Very Slow: Snail Pace",
        slow: "Slow: Cat Pace",
        medium: "Medium: Human Pace",
        fast: "Fast: Ostrich Pace",
        veryFast: "Very Fast: Cheetah Pace"
    }
    const resultMessage = computed(()=>{
        if (props.timer > 500) return resultComments.verySlow
        if (props.timer > 100) return resultComments.slow
        if (props.timer > 50) return resultComments.medium
        if (props.timer > 25) return resultComments.fast
        return resultComments.veryFast
    })
    
    const emit = defineEmits(['changeGameState']);
    emit('changeGameState','end');
</script>

<template>
<div class="result-component">
    <h2>This is your result: {{props.timer}} milliseconds</h2>
    <h3>{{resultMessage}}</h3>
</div>
</template>

<style scoped>
.result-component{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 2rem;
}
</style>