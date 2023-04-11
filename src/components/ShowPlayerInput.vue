<script setup lang="ts">
import { Player } from '../models/Player';
interface IShowPlayer {
    player: Player
}

defineProps<IShowPlayer>();
const emit = defineEmits(["showPlayerInput"]);
</script>



<template></template>
<style scoped></style>