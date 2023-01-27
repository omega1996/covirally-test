<script setup lang="ts">
import Header from './components/Header.vue'
import Board from './components/Board.vue'
</script>

<template>
  <div class="container">
    <Header></Header>
    <Board></Board>
  </div>
</template>

<style scoped lang="scss">
.container {
  width: 1400px;

  @media (max-width: 1400px) {
    width: 1200px;

  }

  @media (max-width: 1200px) {
    width: 1000px;

  }

}
</style>
