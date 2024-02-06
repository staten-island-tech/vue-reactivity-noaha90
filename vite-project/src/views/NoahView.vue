<template>
  <div id="potato">
    <h1 v-for="kid in kids" v-if="check">{{ kid }}</h1>
  </div>
  <button v-if="leck" @click="awesome">
    <P>HELLo</P>
  </button>
</template>

<script setup>
let num = 0
function awesome(){
  document.body.style.backgroundColor = "red"; 
  num++
  console.log(num)
}
const check = false
const leck = true
const kids = ["gabe","noah","nathan","evan","june"]
</script>

<style scoped>
h1{
  font-size: 200px;
}
</style>