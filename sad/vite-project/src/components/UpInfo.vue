
<template>
      <div v-if="display[0].hover === true" class="upgradeinfo"><div id="upleft"><h2>{{ display[0].name }}</h2><p class="upintext">{{ display[0].desc }}</p></div><div id="upright"><h2>{{ display[0].price }}</h2><p class="upintext">{{ display[0].quote }}</p></div></div>
      <div v-else class="upgradeinfo" id="blankmode"><h1>Upgrade Shop</h1></div>
</template>

<script setup>
    const props = defineProps({
    display: Object,
})


</script>




<style lang="css" scoped>
#blankmode{
    text-align: right;
}
.upgradeinfo{
    background-color: #161130;
    justify-content: center;
    color: white;
}
</style>