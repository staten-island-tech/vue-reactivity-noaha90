<template v-if="100 == 4">
    <div class="camp" :id="props.i.text">
      <div class="l">
      <h2>{{ i.text }}</h2>
      <h3>Price: <span class="amount">{{ i.price }}</span></h3>
       <button @click="$emit('add', i)">Hire {{ i.text }}</button> 
    </div>
    <div class="r">
      <h4>{{ i.amount }}</h4>
    </div>
  </div>
  

  </template>
  
  <script setup>
    const props = defineProps({
    i: Object,
})




 </script>
  
  <style lang="css" scoped>
.amount{
  color: #ffd11a;
}
h3,h2,button{
  margin-left: 1.5%;
}
h2{
  color: #ff9b50;
}
.l{
  width: 80%;
}
  .r{
    margin-right: 2%;
    color:#ffffff;
    width: 20%;
    border-color: blue;
    font-size: 20px;
    right: 100%;
    text-align: right;
  }
  .camp{
    color: #ffffff;
    overflow: auto;
    display: flex;
    font-size: .8rem;
    text-align: left;
    background-color:#161130;
    height: 12%;
    border: 3px black solid;
    border-right: 6px black solid;
  }


  h2{
    font-size: 1.5em;
  }
  h3{
    font-size: 1em;
  }
  </style>