<script setup lang="ts">
import { Player } from "../models/Player";
import { ref } from "vue";

const state = ref<Player>(new Player("", "x"));

const emit = defineEmits(["AddPlayerX"]);
const handleClick = () => { emit("AddPlayerX", state.value); };
</script>

<template>
    <div class="player-name">
        <form @submit.prevent>
            <label for="player X">Spelare X</label>
            <input type="text" placeholder="Namn" v-model="state.name">
            <button @click="handleClick">Spara</button>
        </form>
    </div>
</template>
<style scoped>
.player-name {

    display: flex;
    justify-content: space-between;
    gap: 10px;


}
</style> 
