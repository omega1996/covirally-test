<template>
    <div class="board">
        <CardList></CardList>
        <CardList></CardList>
        <CardList></CardList>

    </div>
</template>

<script setup lang="ts">
import CardList from './CardList.vue';
</script>

<style scoped lang="scss">
.board {
    display: flex;
    flex-grow: 1;
    overflow-x: auto;
    flex-grow: 1;
    height: 100%;
    margin-bottom: 20px;
}
</style>
