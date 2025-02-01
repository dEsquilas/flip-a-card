<template>
    <figure class="w-[16px] h-[16px] bg-[url('./../assets/fruits.png')] scale-800"
            :style="getFruit">
    </figure>
</template>
<script setup>
import { computed, defineProps } from 'vue'

const props = defineProps({
    fruit: {
        type: String,
        default: 'coconut'
    }
})

const w = 16
const h = 16

const fruits = {
    "apple": { x: 0, y: 0 },
    "grapes": { x: 3, y: 0 },
    "banana": { x: 6, y: 2 },
    "orange": { x: 9, y: 1 },
    "pear": { x: 10, y: 0 },
    "peach": { x: 12, y: 0 },
    "cherry": { x: 14, y: 1 },
    "pineapple": { x: 11, y: 0 },
    "lemon": { x: 18, y: 2 },
    "strawberry": { x: 27, y: 0 },
    "coconut": { x: 22, y: 4 },

}

const getFruit = computed(() => {

    console.log(props.fruit)

    const x = fruits[props.fruit].x * w
    const y = fruits[props.fruit].y * h

    return {
        backgroundPosition: `-${x}px -${y}px`,
        width: `${w}px`,
        height: `${h}px`
    }

})

</script>