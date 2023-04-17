<script setup lang="ts">
import { Player } from '../models/Player';
import { ref } from 'vue';

import TickTackGame from "./TickTackGame.vue"

const emit = defineEmits(["backToGame", "startNew"]);
const reset = ref(false);
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

const resetGame = () => {
    reset.value = true;

}


</script>
<template>
    <div v-if="!reset" class="score">
        <div class="players">
            <div class="headers">
                <p>Namn:</p>
                <p>Poäng:</p>
            </div>

            <div class="playerX">
                <p>{{ props.players[0].name }}</p>
                <p v-if="props.winners && props.winners.find(winner => winner.name === props.players[0].name)">{{
                    props.players[0].score }}</p>
                <p v-else>0</p>
            </div>

            <div class="playerO">
                <p>{{ props.players[1].name }}</p>
                <p v-if="props.winners && props.winners.find(winner => winner.name === props.players[1].name)">{{
                    props.players[1].score }}</p>
                <p v-else>0</p>
            </div>


        </div>
        <div class="navigation">
            <button @click="$emit(`backToGame`)">Visa spel</button>
            <button @click="$emit(`startNew`)">Borja nytt spel</button>
            <button @click="resetGame">Börja om från början</button>
        </div>
    </div>
    <TickTackGame v-else></TickTackGame>
</template>
<style scoped>
.players {
    display: flex;
    justify-content: space-around;
    margin-bottom: 30px;
    gap: 10px;
}

.headers {
    font-weight: bold;
    margin-right: 20px;
}

.navigation {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
}
</style>

