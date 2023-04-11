<script setup lang="ts">
</script>

<template>
    <div>
        <form @submit.prevent class="player-name">
            <span>Spelare X</span>
            <input type="text" placeholder="Name">
            <button>Spara</button>
        </form>
    </div>

    <div>
        <form @submit.prevent class="player-name">

            <span>Spelare 0</span>
            <input type="text" placeholder="Name">
            <button>Börja spelet</button>
        </form>
    </div>
</template>
<style scoped>
.player-name {

    display: flex;
    justify-content: space-around;

}
</style> 
