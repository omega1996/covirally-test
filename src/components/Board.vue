<template>
    <div class="board">
        <CardList @addNewList="addNewList" v-for="board in boardData" :list="board.cardList" :listName="board.listName">
        </CardList>
    </div>
</template>

<script setup lang="ts">
import CardList from './CardList.vue';
import { ref, onMounted } from 'vue'
import type { CardType } from './Card.vue'

interface ColumnType {
    cardList: CardType[],
    listName: string
}

function addNewList(event: any) {
    console.log(event)
}

const boardData = ref<ColumnType[]>()
onMounted(() => {
    boardData.value = [
        {
            cardList: [{ name: 'Проверить тестовое' }],
            listName: "В очереди"
        },
        {
            cardList: [{ name: 'Написать тестовое' }],
            listName: "В работе"
        },
        {
            cardList: [{ name: 'Выслать тестовое' }],
            listName: "Сделано"
        },

    ]
})


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
