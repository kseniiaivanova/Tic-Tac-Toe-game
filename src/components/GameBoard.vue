<script setup lang="ts">

import { Player } from '../models/Player';
import { ref } from 'vue';
import Score from './Score.vue';


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

let winners = ref<Player[]>([]);

let hideScore = ref(true);
let win = ref(false);

const findWinner = () => {

    for (let i = 0; i < winningCombinations.length; i++) {

        const [a, b, c] = winningCombinations[i];
        if (gameBoard.value[a] && gameBoard.value[a] === gameBoard.value[b] && gameBoard.value[a] === gameBoard.value[c]) {
            winner.value = currentPlayer.value;
            gameOver.value = true;
            currentPlayer.value!.score++;
            winners.value.push(currentPlayer.value!);

            win.value = true;

            return winner.value;

        }
    }

    const isBoardFull = gameBoard.value.every(cell => cell !== '');
    if (isBoardFull) {

        gameOver.value = true;
        win.value = false;

        return null;

    }

};





const togglePlayer = () => {

    if (currentPlayer.value === props.players[0]) {
        currentPlayer.value = props.players[1]

    } else {
        currentPlayer.value = props.players[0]
    }

};






const handleClick = (index: number) => {

    if (!gameOver.value && !gameBoard.value[index]) {
        gameBoard.value[index] = currentPlayer.value!.role;
        findWinner();

        if (winner.value) {
            gameOver.value = true;
        }

        console.log(gameOver.value);
        console.log(winner.value);




        if (!gameOver.value) {
            togglePlayer();

        }




    }




};



const restart = () => {
    gameBoard.value = Array(9).fill('');
    currentPlayer.value = props.players[Math.floor(Math.random() * 2)];
    winner.value = undefined;
    gameOver.value = false;

};


const startNew = () => {
    backToGame();
    restart();

};


const showScore = () => {
    console.log("Du klickade på Score")
    hideScore.value = false;
};

const backToGame = () => {
    hideScore.value = true;


}

</script>


<template>
    <div class="wrapper" v-if="hideScore">
        <h3>Tic Tac Toe Game</h3>


        <div v-if="!gameOver && currentPlayer">
            <p v-if="!gameOver && currentPlayer">Det är {{ currentPlayer.name }}s tur</p>

        </div>
        <div v-else>

            <p class="win" v-if="win">Grattis {{ currentPlayer!.name }}! Du vann!</p>


            <p class="draw" v-else>DRAW!</p>
        </div>

        <div class="gameboard">

            <div class="tile" v-for="(cell, index) in gameBoard" :key="index" @click="handleClick(index)">
                {{ cell }}
            </div>

        </div>

        <button v-if="gameOver" @click="restart">Börja nytt spel</button>
        <button @click="showScore">Visa poäng</button>

    </div>
    <Score v-else :winners="winners" :players="players" @back-to-game="backToGame" @start-new="startNew"></Score>
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
