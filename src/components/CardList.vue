<template>

    <div class="card-list">
        <div class="card-list__container">
            <draggable class="list-group" :list="list" group="people" itemKey="name">
                <template #item="{ element, index }">
                    <Card :card="element"></Card>
                </template>
            </draggable>

        </div>
    </div>
</template>

<script setup lang="ts">
//@ts-ignore
import draggable from "vuedraggable";
import Card from './Card.vue';
import { ref, onMounted } from "vue"
import type { CardType } from './Card.vue'

const list = ref<CardType[]>([])

onMounted(() => {
    list.value = [
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 }
    ]
})

</script>

<style scoped lang="scss">
.card-list {
    width: 300px;
    min-height: 200px;
    flex-shrink: 0;

    &__container {
        padding: 20px 10px;
        margin-right: 10px;
        border-radius: 4px;
        background: #8f8f8f;

    }
}
</style>
