<template>
    <section class="bg-green-700 w-dvw h-dvh grid grid-cols-4 gap-4 p-4">
        <Card :data="card" v-for="(card, index) in cards" :key="index" />
    </section>
</template>

<script setup>
import { ref } from 'vue'
import Card from './components/Card.vue'

const fruits = [
    "apple", "grapes", "banana", "orange", "pear", "peach", "cherry", "pineapple", "lemon", "strawberry", "coconut"
]

const cards = ref([])
const tapeLength = 12

let availablePosition = []

const getEmptyPosition = (positions) => {
    const randomIndex = Math.floor(Math.random() * positions.length)
    const position = positions[randomIndex]
    positions.splice(randomIndex, 1)
    return position
}

const init = () => {

    for (let i = 0; i < tapeLength; i++) {
        availablePosition.push(i)
    }

    console.log(availablePosition)

    for (let i = 0; i < tapeLength / 2; i++) {
        const c1 = getEmptyPosition(availablePosition)
        const c2 = getEmptyPosition(availablePosition)

        const fruit = fruits[Math.floor(Math.random() * fruits.length)]

        fruits.splice(fruits.indexOf(fruit), 1)

        cards.value.push({ fruit: fruit, position: c1 })
        cards.value.push({ fruit: fruit, position: c2 })
    }

    cards.value.sort((a, b) => a.position - b.position)
}


init()

</script>