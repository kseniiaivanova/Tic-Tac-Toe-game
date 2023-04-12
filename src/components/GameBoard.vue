<script setup lang="ts">

import { Player } from '../models/Player';
import { ref } from 'vue';

const props = defineProps<IPlayers>();

interface IPlayers {

    players: Player[];

};

const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
];



let gameBoard = ref<string[]>(Array(9).fill(''));

let currentPlayer = ref<Player>();

currentPlayer.value = props.players[0];

let winner = ref<Player>();

let gameOver = ref(false);

const findWinner = () => {

    for (let i = 0; i < winningCombinations.length; i++) {
        const [a, b, c] = winningCombinations[i];
        if (gameBoard.value[a] && gameBoard.value[a] === gameBoard.value[b] && gameBoard.value[a] === gameBoard.value[c]) {
            winner.value = currentPlayer.value;
            gameOver.value = true;
            break;
        }
    }

};

const togglePlayer = () => {
    currentPlayer.value = currentPlayer.value === props.players[0] ? props.players[1] : props.players[0];
};


const handleClick = (index: number) => {


    if (!gameOver.value && !gameBoard.value[index]) {
        gameBoard.value[index] = currentPlayer.value!.role;
        findWinner();

        if (!gameOver.value) {
            togglePlayer();
        }
    }

};





</script>

<template>
    <div class="container">
        <div class="tile" v-for="(cell, index) in gameBoard" :key="index" @click="handleClick(index)">
            {{ cell }}
        </div>

    </div>
</template>
<style scoped>
.container {
    display: flex;
    flex-wrap: wrap;
    width: 400px;
    gap: 2px;
}

.tile {

    width: 100px;
    height: 100px;
    background-color: aqua;
}
</style>
