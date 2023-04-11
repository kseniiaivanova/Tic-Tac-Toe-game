<script setup lang="ts">
import { Player } from "../models/Player";
import { ref } from "vue";

const state = ref<Player[]>([new Player("", "x"), new Player("", "0")]);
</script>

<template>
    <div>
        <form @submit.prevent class="player-name">
            <span>Spelare X</span>
            <input type="text" placeholder="Name" v-model="state[0].name">
            <button>Spara</button>
        </form>
    </div>

    <div>
        <form @submit.prevent class="player-name">

            <span>Spelare 0</span>
            <input type="text" placeholder="Name" v-model="state[1].name">
            <button>Börja spelet</button>
        </form>
    </div>
</template>
<style scoped>
.player-name {

    display: flex;
    justify-content: space-between;
    align-items: center;

}
</style> 
