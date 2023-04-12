<script setup lang="ts">
import { Player } from '../models/Player';
import { ref } from 'vue';

const state = ref<Player>(new Player("", "0"));
const emit = defineEmits(["AddPlayerO"]);
const handleClick = () => { emit("AddPlayerO", state.value); };

</script>


<template>
    <div>
        <form @submit.prevent>

            <label for="spelare 0">Spelare 0</label>
            <input type="text" placeholder="Namn" v-model="state.name">
            <button @click="handleClick">Börja spelet</button>
        </form>
    </div>
</template>