<script setup lang="ts">
import PlayerInputX from './PlayerInputX.vue';
import PlayerInputO from './PlayerInputO.vue';


const handleClick = (i: number, event: MouseEvent) => {
    console.log("Du klickade på knappen", i, event);
};
</script>

<template>
    <div class="container">
        <div class="tile" v-for="i in 9" @click="handleClick(i, $event)">

        </div>
    </div>
</template>
<style scoped>
.container {
    display: flex;
    flex-wrap: wrap;
    width: 400px;
    gap: 2px;
}

.tile {

    width: 100px;
    height: 100px;
    background-color: aqua;
}
</style>
