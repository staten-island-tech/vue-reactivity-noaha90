<template>
    <div>
        <button class="choice" :id="props.tab" @click="$emit('switch', tab)">{{ tab }}</button>
    </div>
</template>

<script setup>
    const props = defineProps({
    tab: String,
    test: Number,
})




</script>




<style lang="css" scoped>
.choice{
    overflow: auto;
}
.choice:hover{
    transition: .65s;
    background-color: rgba(200,43,100,0.3);
}
</style>