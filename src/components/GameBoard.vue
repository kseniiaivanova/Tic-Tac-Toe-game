<script setup lang="ts">

import { Player } from '../models/Player';
import { ref } from 'vue';
import { watch } from 'vue';

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



const restart = () => {
    gameBoard.value = Array(9).fill('');
    currentPlayer.value = props.players[0];
    winner.value = undefined;
    gameOver.value = false;

};
</script>

<template>
    <div class="wrapper">
        <h3>Tic Tac Toe Game</h3>
        <p v-if="currentPlayer">Det är {{ currentPlayer.name }}s tur</p>
        <div class="gameboard">
            <div class="tile" v-for="(cell, index) in gameBoard" :key="index" @click="handleClick(index)">
                {{ cell }}
            </div>

        </div>
        <button v-if="gameOver" @click="restart">Börja om från början</button>
    </div>
</template>

<style scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
}

.gameboard {

    display: flex;
    flex-wrap: wrap;
    width: 306px;
    gap: 2px;
}

.tile {

    width: 100px;
    height: 100px;
    background-color: aqua;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3em;
}
</style>
