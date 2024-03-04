
<template>
<p>Lifetime Prestige: {{ Math.round(stats[0].lifetime) }}</p>
<p>Click Power: {{ stats[0].power }}</p>
<p>Prestige Per Second: {{ stats[0].PPS }}</p>
<p>Team Size: {{ stats[0].team }}</p>
<p>Achievements: WIP</p>
</template>

<script setup>
    const props = defineProps({
    stats: Object,
})
</script>




<style lang="css" scoped>
p{
    color: chartreuse;
}

.audioText{
    color: white;
}

</style>