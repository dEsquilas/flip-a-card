<template>
    <section class="bg-green-700">
        <section class="flex items-center justify-center h-screen text-white" v-show="!initedGame">
            <button class="bg-green-800 px-8 py-4 rounded-xl text-4xl cursor-pointer hover:bg-green-900 transition" @click="startGame">
                Start Game
            </button>
        </section>
        <section class="flex flex-col items-center justify-center w-dvw h-dvh" v-show="initedGame">
            <h2 class="text-4xl text-center w-full text-white text-left pl-4">Time: {{ timer }}</h2>
            <section class="w-full grid grid-cols-[repeat(auto-fill,_minmax(200px,_1fr))] auto-rows-min gap-4 p-4">
                <Card :data="card" v-for="(card, index) in cards" :key="index" @click="flipCard(card)" />
            </section>
        </section>
    </section>
</template>
<script setup>
/* eslint-disable */
import { computed, ref } from 'vue'
import Card from './components/Card.vue'

const fruits = [
    "apple", "grapes", "banana", "orange", "pear", "peach", "cherry", "pineapple", "lemon", "strawberry", "coconut"
]

const cards = ref([])
const initedGame = ref(false)
const delta = ref(0)
const tapeLength = 12
let lastCard = null
let timerInterval = null


let availablePosition = []

const getEmptyPosition = (positions) => {
    const randomIndex = Math.floor(Math.random() * positions.length)
    const position = positions[randomIndex]
    positions.splice(randomIndex, 1)
    return position
}

const flipCard = (card) => {

    if(card.isFlipped) return

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

    for(let i = 0; i < cards.value.length; i++){
        if(!cards.value[i].isFlipped){
            return
        }
    }

    clearInterval(timerInterval)
    alert(`You win! Time: ${getTime()}`)


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

const startGame = () => {
    initedGame.value = Date.now()
    timerInterval = setInterval(function() {
        delta.value = Date.now() - initedGame.value; // milliseconds elapsed since start
    }, 10); // update about every second
}

const getTime = () => {
    const t = Math.floor(delta.value / 1000)

    const minutes = String(Math.floor(t / 60)).padStart(2, '0')
    const seconds = String(t % 60).padStart(2, '0')
    const miliseconds = String(delta.value % 1000).padStart(3, '0')

    return `${minutes}:${seconds}:${miliseconds}`
}

const timer = computed(() => {
    return getTime()
})


init()

</script>