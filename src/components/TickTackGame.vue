<script setup lang="ts">
import PlayerInputX from './PlayerInputX.vue';
import { Player } from "../models/Player";
import PlayerInputO from './PlayerInputO.vue';
import GameBoard from './GameBoard.vue';
import { ref } from 'vue';
import Score from './Score.vue';

let players = ref<Player[]>([]);

let show = ref(true);

let showInputs = ref(true);


const addPlayerX = (playerX: Player) => {
    console.log(playerX);
    players.value.push(playerX);
    show.value = false;


}


const addPlayerO = (playerO: Player) => {

    showInputs.value = false;
    players.value.push(playerO);


}

</script>

<template>
    <div v-if="showInputs">
        <PlayerInputX v-if="show" @add-player-x="addPlayerX"></PlayerInputX>
        <PlayerInputO v-else @add-player-o="addPlayerO"></PlayerInputO>
    </div>
    <GameBoard :players="players" v-else></GameBoard>
</template>
<style></style>