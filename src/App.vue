<template>
    <section class="bg-green-700 w-dvw h-dvh grid grid-cols-3 gap-4 p-4">
        <Card :data="card" v-for="(index, card) in cards" :key="index" />
    </section>
</template>

<script setup>
import Card from './components/Card.vue'
import { ref } from 'vue'

const cards = ref([1,2,3,4,5,6,7,8,9])

</script>