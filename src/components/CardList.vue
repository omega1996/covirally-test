<template>

    <div class="card-list">
        <div class="card-list__container">
            <draggable animation="200" class="list-group" :list="list" group="people" itemKey="name">
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

        </div>
    </div>
</template>

<script setup lang="ts">
//@ts-ignore
import draggable from "vuedraggable";
import Card from './Card.vue';
import { ref, onMounted, watch } from "vue"
import type { CardType } from './Card.vue'

const list = ref<CardType[]>([])
const newCardName = ref('')
const hasError = ref(false)
const listName = ref('list name')

onMounted(() => {
    list.value = [
        { name: "John" },
        { name: "Joao" },

    ]
})

watch(newCardName, () => {
    hasError.value = false
})

function add() {
    if (newCardName.value) {

        list.value.push({ name: newCardName.value });
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

    &__header {
        margin-bottom: 10px ;
    }

    &__container {
        padding: 20px 10px;
        margin-right: 10px;
        border-radius: 4px;
        background: #c6c6c6;

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
