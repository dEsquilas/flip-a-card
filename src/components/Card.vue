<template>
    <article class="flip-card perspective-1000 relative width-1/3 aspect-[12/16] cursor-pointer group">
        <div class="flip-card-inner w-full h-full transform-3d transition-[transform] duration-800"
            :class="{
                       'rotate-y-180': data.isFlipped,
                       'group-hover:rotate-y-30': !data.isFlipped }"
        >
            <div class="flip-card-front absolute w-full h-full backface-hidden

                        border-1 border-black bg-white p-4 rounded-2xl flex items-center justify-content
                        ">
                <div class="border border-black w-full h-full bg-green-900 rounded-xl flex items-center justify-center">
                </div>

            </div>
            <div class="flip-card-back px-3 py-3 bg-white absolute w-full h-full backface-hidden rotate-y-180
                        border border-black rounded-2xl flex items-center justify-content
                        ">
                <div class="border border-black w-full h-full bg-red-500 rounded-xl flex items-center justify-center">
                    <fruit :fruit="data.fruit" />
                </div>
            </div>
        </div>
    </article>
</template>
<script setup>
import { defineProps } from 'vue'
import Fruit from './Fruit.vue'

defineProps({
    data: {
        type: Object,
        required: true
    }
})

</script>