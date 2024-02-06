<template>
  <div id="potato">
    <!-- <h1 v-for="kid in kids" v-if="check">{{ kid }}</h1> -->
    <h2>{{ count }}</h2>
  </div>
  <button v-if="leck" @click="awesome">
    <P>HELLo</P>
  </button>
</template>

<script setup>
import { ref } from "vue"
const kids = ["gabe","noah","evan","june","nathan","ben"]
const count = ref(kids[0])
count.index = 0
console.log(count)
let check = true    
function awesome(){
  if(count.index < kids.length - 1){
    count.index++
    count.value = kids[count.index]
    console.log(count.index)
  }
  else{
    count.index = 0
    count.value = kids[count.index]
  }
}
const leck = true
</script>

<style lang="scss" scoped>
h1{
  font-size: 20px;
}
</style>