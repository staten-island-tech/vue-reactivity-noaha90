<template>
    <div v-for="goal in goals">
        <div class="goalbox" :class="goal.rank" v-if="goal.p1 >= goal.p2"><h2>{{ goal.title }}</h2><h3>{{ goal.desc }}</h3></div>
        <img class="goalbox locked" v-if="goal.p1 < goal.p2" src="https://www.donaldson.com/content/dam/donaldson/shared-assets/icons-pictograms/Question-Mark.jpg/jcr:content/renditions/cq5dam.web.1280.1280.jpeg">
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

.rare{
    background-color: crimson;
}
.goalbox{
    border: 3px black solid;
    color: black;

}
.locked{
    height: 64px;
    width: 64px;
}
</style>