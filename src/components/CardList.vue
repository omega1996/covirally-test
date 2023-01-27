<template>

    <div class="card-list">
        <div class="card-list__container">
            <div @click="addList(true)" class="card-list__add-list">
                +
            </div>
            <draggable animation="200" class="card-list__list-group" :list="list" group="people" itemKey="name">
                <template #header>
                    <div class="card-list__header">

                        {{ listName }}
                    </div>
                </template>
                <template #item="{ element, index }">
                    <Card :card="element"></Card>
                </template>
                <template #footer>
                    <input :class="{ 'card-list__add-input--error': hasError }" class="card-list__add-input"
                        v-model="newCardName" placeholder="Имя карточки">
                    <button class="card-list__add-button" @click="add">Добавить</button>
                </template>
            </draggable>
            <div @click="addList(false)" class="card-list__add-list">+</div>

        </div>
    </div>
</template>

<script setup lang="ts">
//@ts-ignore
import draggable from "vuedraggable";
import Card from './Card.vue';
import { ref, watch, PropType } from "vue"
import type { CardType } from './Card.vue'

const newCardName = ref('')
const hasError = ref(false)
const emit = defineEmits(['addNewList'])


function addList(before: boolean) {
    emit('addNewList', { before, "listName": props.listName })
}


const props = defineProps({
    listName: {
        type: String
    },
    list: {
        type: Object as PropType<CardType[]>
    }
})

watch(newCardName, () => {
    hasError.value = false
})

function add() {
    if (newCardName.value) {
        props.list?.push({ name: newCardName.value });
        newCardName.value = ''
    } else {
        hasError.value = true
    }
}

</script>

<style scoped lang="scss">
.card-list {
    width: 300px;
    min-height: 200px;
    flex-shrink: 0;

    &__list-group {
        flex-grow: 1;
        margin: 0 5px;
    }

    &__add-list {
        display: flex;
        background: rgb(151, 151, 151);
        transition: all 0.2s;
        width: 10px;
        border-radius: 4px;
        align-items: center;
        justify-content: center;
        cursor: pointer;


        &:hover {
            width: 20px;
        }
    }

    &__header {
        margin-bottom: 10px;
    }

    &__container {
        padding: 10px 2px;
        margin-right: 10px;
        border-radius: 4px;
        background: #c6c6c6;
        display: flex;
    }

    &__add-button {
        width: 100%;
        background: white;
        border-radius: 4px;
    }

    &__add-input {
        width: 100%;
        box-sizing: border-box;

        &--error {
            outline: 1px solid red;
        }
    }
}
</style>
