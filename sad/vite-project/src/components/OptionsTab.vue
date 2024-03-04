
<template>
    <form id="control">
        <h2 class="audioText">Audio Controls</h2>
         <input type="range" min="0" max="100" value="50" id="slider" @change="$emit('volume')">
        <div v-for="i in audio.length">
        <input type="radio" class="check"  name="music" @change="$emit('music',audio[i-1])" :value="audio[i-1]"><label class="audioText">{{ audio[i-1].name }}</label><br>
    </div>
    
      </form> 
      <form id="cheats">
        <h2 class="audioText">Cheats</h2>
        <input id='cForm' type="text"  @submit.prevent="$emit('cheat',text)"><br>
        <button @click.prevent="$emit('cheat',text)">eaeaea</button>
      </form> 
      <div id="stat">
        <h2>Stats</h2>
      <p>Lifetime Prestige: {{ Math.round(stats[0].lifetime) }}</p>
    <p>Click Power: {{ stats[0].power }}</p>
    <p>Prestige Per Second: {{ stats[0].PPS }}</p>
    <p>Team Size: {{ stats[0].team }}</p>
</div>
    </template>

    <script setup>
        const props = defineProps({
        audio: Object,
        stats: Object,
    })
    console.log(0/10)
    </script>
    
    
    
    
    <style lang="css" scoped>
    .audioText{
        color: white;
    }
    input{
        text-align: center;
    }
    #control,#cheats,#stat{
        border-bottom: 6px #2f2a49 solid;
        background-color: #161130;
    }
    #stat{
        min-height: 35%;
        display: flex;
        align-items: center;
        flex-direction: column;
        justify-content: space-evenly;
        color: #ffffff;
    }

    </style>