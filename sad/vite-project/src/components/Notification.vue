<template>
    <div v-for="goal in goals">
       <div class="notification" :class="goal.rank" :id="goal.title.replaceAll(' ', '')" v-if="goal.p1 >= goal.p2">
        <h2>Achievement Get!</h2>
        <h3>{{ goal.title }}</h3>
        <img src="https://svgsilh.com/png-512/31226.png" @click="$emit('close',goal.title.replaceAll(' ', ''))">
    </div>
    </div>
</template>

<script setup>
    const props = defineProps({
    goals: Object,
})
console.log(props.goals)
</script>

<style lang="css" scoped>

.common{
    background-color: greenyellow;
}
.uncommon{
    background-color: lightcyan;
}

.notification{
    width: 25%;
    height: 8.5%;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    border: black 2px solid;
  position: absolute;
  top: 0%;
  left: 50%;
  transform: translate(-50%, 0%);
}

img{
    position: absolute;
    right: 1%;
    top: 3%;
    height: 25%;
    width: auto;
}
.rare{
    background-color: crimson;
}
h2{
    font-size: 1.5em;
}
h3{
    font-size: .8em;
}
</style>