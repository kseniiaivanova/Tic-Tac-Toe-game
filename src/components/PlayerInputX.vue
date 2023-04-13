<script setup lang="ts">
import { Player } from "../models/Player";
import { ref } from "vue";

const state = ref<Player>(new Player("", "X", 0));

const emit = defineEmits(["AddPlayerX"]);
const handleClick = () => { emit("AddPlayerX", state.value); };
</script>

<template>
    <h3>Tic Tac Toe Game</h3>


    <form @submit.prevent class="player-name">
        <label for="player X">Spelare X</label>
        <input type="text" placeholder="Namn" v-model="state.name">
        <button @click="handleClick">Spara</button>
    </form>
</template>
<style scoped>
.player-name {

    display: flex;
    justify-content: space-around;
    align-items: center;

    gap: 10px;


}
</style> 
