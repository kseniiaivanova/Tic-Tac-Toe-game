<script setup lang="ts">

import { Player } from '../models/Player';
import GameBoard from './GameBoard.vue';

const emit = defineEmits(["backToGame", "startNew"]);



const props = defineProps({
    winners: {
        type: Array as () => Player[],
        required: true
    },
    players: {
        type: Array as () => Player[],
        required: true
    }
});


</script>
<template>
    <div class="wrapper">
        <div class="playerX">
            <p>{{ props.players[0].name }}</p>
            <p v-if="props.winners && props.winners.length && props.players[0].name === props.winners[0].name"> {{
                props.winners[0].score }}</p>

        </div>

        <div class="playerO">
            <p>{{ props.players[1].name }}</p>
            <p v-if="props.winners && props.winners.length > 1 && props.players[1].name === props.winners[1].name"> {{
                props.winners[1].score }}</p>
        </div>

    </div>
    <button @click="$emit(`backToGame`)">Visa spel</button>
    <button @click="$emit(`startNew`)">Borja nytt spel</button>
</template>
<style scoped>
.wrapper {
    display: flex;
    justify-content: space-around;



}
</style>

