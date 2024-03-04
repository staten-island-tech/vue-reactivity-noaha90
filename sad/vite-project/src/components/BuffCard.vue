
<template>
       <img class="cardImage" v-if="info.show.value" :src=info.url @click="$emit('buy', info)" @mouseenter="$emit('display',info)" @mouseleave="$emit('defaultmenu')"> 
</template>

<script setup>
    const props = defineProps({
    info: Object,
})


</script>




<style lang="css" scoped>


.cardImage{
    display: flex;
    align-items: end;
    height: 100%;
    width: auto;
    border: 2px solid black;
    background-color: #161130;
    aspect-ratio: 1 / 1;
}
.cardImage:hover{
    transition: .75s;
    background-color: rgba(250,250,124,0.99);
}
</style>


<!-- 
<template>
    <div class="test">
       <img class="cardImage" :src=info.url @click="$emit('buy', info)" @mouseenter="$emit('display',info)" @mouseleave="$emit('defaultmenu')">
    </div>
</template>

<script setup>
    const props = defineProps({
    info: Object,
})

console.log(props)


</script>




<style lang="css" scoped>

.test{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 16vh;
    padding: .5%;
    border: 2px solid black;
    background-color: rgba(52,43,124,0.7);
    aspect-ratio: 1 / 1;
}
.cardImage{
    position: relative;
    top: 4%;
    height: 95%;
    width: auto;
    aspect-ratio: 1 / 1;
}


.test:hover{
    transition: .75s;
    background-color: rgba(250,250,124,0.7);
}
</style> -->