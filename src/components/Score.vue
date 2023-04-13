<script setup lang="ts">

import { Player } from '../models/Player';
import GameBoard from './GameBoard.vue';

let props = defineProps<IWinners>();

interface IWinners {

    winners: Player[];

};

</script>
<template>
    <div class="wrapper">
        <p v-if="props.winners && props.winners.length"> {{ props.winners[0].name }}</p>
        <p v-if="props.winners && props.winners.length"> {{ props.winners[0].score }}</p>
        <p v-if="props.winners && props.winners.length > 1"> {{ props.winners[1].name }}</p>
        <p v-if="props.winners && props.winners.length > 1"> {{ props.winners[1].score }}</p>
    </div>
    <button>Visa spel</button>
    <button>Borja nytt spel</button>
</template>
<style scoped>
.wrapper {
    display: flex;

}
</style>

