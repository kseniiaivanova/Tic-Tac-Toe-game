<script setup lang="ts">
import { Player } from '../models/Player';
import { ref } from 'vue';

const state = ref<Player>(new Player("", "0"));
</script>


<template>
    <div>
        <form @submit.prevent>

            <span>Spelare 0</span>
            <input type="text" placeholder="Namn" v-model="state.name">
            <button>Börja spelet</button>
        </form>
    </div>
</template>