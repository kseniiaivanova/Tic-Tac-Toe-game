<script setup lang="ts">
import PlayerInputX from './PlayerInputX.vue';
import ShowPlayerInput from './ShowPlayerInput.vue';
import { Player } from "../models/Player";
import PlayerInputO from './PlayerInputO.vue';
import GameBoard from './GameBoard.vue';
import { ref } from 'vue';

const show = ref(false);

const showBoard = ref(false);

let players = ref<Player[]>([]);
</script>

<template>
    <div v-if="showBoard!">
        <PlayerInputX v-if="show"></PlayerInputX>
        <PlayerInputO v-else></PlayerInputO>
    </div>
    <GameBoard v-else></GameBoard>
</template>
<style></style>