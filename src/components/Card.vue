<template>
    <article class="flip-card perspective-1000 relative width-1/3 aspect-ratio-[9/16] ">
        <div class="flip-card-inner w-full h-full transform-3d">
            <div class="flip-card-front">
                FRONT
            </div>
            <div class="flip-card-back">
                BACK
            </div>
        </div>
    </article>
</template>
<style lang="scss">
/* This container is needed to position the front and back side */
.flip-card-inner {
    text-align: center;
    transition: transform 0.8s;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front, .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden; /* Safari */
    backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
    background-color: #bbb;
    color: black;
}

/* Style the back side */
.flip-card-back {
    background-color: dodgerblue;
    color: white;
    transform: rotateY(180deg);
}
</style>