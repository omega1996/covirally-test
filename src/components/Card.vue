<template>
    <div class="card">
        {{ card?.name }}
    </div>
</template>

<script setup lang="ts">
import { ref, PropType } from 'vue'


export interface CardType {
    name: string,
    id: number
}

const props = defineProps({
    card: {
        type: Object as PropType<CardType>
    }
})
const cardName = ref('card name')
</script>

<style scoped lang="scss">
.card {
    background: white;
    width: 100%;
    min-height: 30px;
    margin-bottom: 10px;
    border-radius: 4px;
    padding: 4px;
    box-sizing: border-box;
}
</style>
