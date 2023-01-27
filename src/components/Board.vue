<template>
    <div class="board">
        <CardList @saveName="changeCardName" @addNewList="addNewList" v-for="board in boardData" :list="board.cardList"
            :listName="board.listName">
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

function changeCardName(event: any) {
    const cardList = boardData.value?.find((element) => element.listName == event.old)
    if (cardList) {
        cardList.listName = event.new
    }
}

function addNewList(event: any) {
    const index = boardData.value?.findIndex((element) => element.listName == event.name)
    if (index !== -1 && index !== undefined) {
        boardData.value?.splice(event.before ? index : index + 1, 0, {
            cardList: [],
            listName: "Новая карточка"
        })
    }
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
    box-sizing: border-box;
    padding-bottom: 20px;
}
</style>
