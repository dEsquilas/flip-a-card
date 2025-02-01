<template>
    <div class="flex items-center justify-center w-dvw h-dvh bg-green-700 ">
        <section class="w-full grid grid-cols-4 auto-rows-min gap-4 p-4">
            <Card :data="card" v-for="(card, index) in cards" :key="index" @click="flipCard(card)" />
        </section>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import Card from './components/Card.vue'

const fruits = [
    "apple", "grapes", "banana", "orange", "pear", "peach", "cherry", "pineapple", "lemon", "strawberry", "coconut"
]

const cards = ref([])
const tapeLength = 12
let lastCard = null

let availablePosition = []

const getEmptyPosition = (positions) => {
    const randomIndex = Math.floor(Math.random() * positions.length)
    const position = positions[randomIndex]
    positions.splice(randomIndex, 1)
    return position
}

const flipCard = (card) => {

    card.isFlipped = true

    if(lastCard === null){
        lastCard = card
    }
    else{
        if(lastCard.fruit === card.fruit){
            lastCard = null
        }
        else{
            setTimeout(() => {
                lastCard.isFlipped = false
                card.isFlipped = false
                lastCard = null
            }, 500)
        }
    }



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

        cards.value.push({ fruit: fruit, position: c1, isFlipped: false })
        cards.value.push({ fruit: fruit, position: c2, isFlipped: false })
    }

    cards.value.sort((a, b) => a.position - b.position)
}


init()

</script>