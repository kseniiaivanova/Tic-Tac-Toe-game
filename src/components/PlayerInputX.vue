<script setup lang="ts">
import { Player } from "../models/Player";
import { ref } from "vue";

const state = ref<Player>(new Player("", "x"));
</script>

<template>
    <div class="player-name">
        <form @submit.prevent>
            <span>Spelare X</span>
            <input type="text" placeholder="Namn" v-model="state.name">
            <button>Spara</button>
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
