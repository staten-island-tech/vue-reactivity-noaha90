<script setup>
import {getCurrentInstance, ref} from "vue"
import ArmyGalVue from '@/components/ArmyGal.vue';
import NavBar from "@/components/NavBar.vue";
import BuffCard from "@/components/BuffCard.vue";
import StatsTab from "@/components/StatsTab.vue";
import UpInfo from "@/components/UpInfo.vue";
import OptionsTab from "@/components/OptionsTab.vue";
import AchievementTab from "@/components/AchievementTab.vue";
import Notification from "@/components/Notification.vue";
import { state } from '@/components/state'
</script>

<script>

let startedMusic = ref(false)
let tabs = ["options","achievements"]
let prestige = ref(0)
const mode = ref("options")
let multiplier = ref(0)
let team = ref(0)
let click = ref(1 + (team.value/10))
let lifetime = ref(0)
let clickMulti = []


// score = value/price
let array = [{
  text: "Freshmen",
  value: 0.001,
  price: 45,
  og: 45,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [2,3]
},
{
  text: "Antisocial Redditor",
  value: 0.03,
  price: 175,
  og: 175,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [4,5]
},
{
  text: "Unpaid Intern",
  value: 0.1,
  price: 750,
  og: 750,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{
  text: "Youtube Tutorial",
  value: 0.4,
  price: 5600,
  og: 5600,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{
  text: "Stack Overflow",
  value: 4,
  price: 30000,
  og: 30000,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{
  text: "Chat GPT",
  value: 12 ,
  price: 1200000,
  og: 1200000,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{
  text: "Paid Intern",
  value: 35,
  price: 8400000,
  og: 840000,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{
  text: "IIT Graduate",
  value: 8000,
  price: 25500000,
  og: 25500000,  
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
{ 
  text: "Woman",
  value: 3500,
  price: 300000000,
  og: 300000000,
  amount: ref(0),
  multipliers: [],
  discounts: [],
  newUps: [1,2,3]
},
]

console.log(array)


let upInfo = [
{
      price: 889000,
        url: "https://i.imgur.com/JvSGjw2.png",
        effect: ["global",1.05],
        id: "Noah-Rozin",
        quote: "Increases Global Production By 5%",
        desc: "Hi",
        show: ref(true),
       },
{
  price: 2500,    
 url: "https://cdn.icon-icons.com/icons2/2157/PNG/512/github_git_hub_logo_icon_132878.png",
 effect: ["click",2],
 id: "Github-Desktop",
 quote: "The Other Ultimate Tool For Coders",
 desc: "Improves Clicking Power By 200%",
 show: ref(true), //keep
},
{
  price: 64000,    
 url: "https://images.fineartamerica.com/images/artworkimages/medium/3/ethernet-cables-vector-tim-hester-transparent.png",
 effect: ["percent",3,2],
 id: "Ethernet-Cable",
 quote: "Premium Wifi",
 desc: "Improves Youtube Tutorials By 200%",
 show: ref(true), //keep
},
{
  price: 8500,
 url: "https://cdn-icons-png.flaticon.com/512/4650/4650660.png",
 effect: ["percent",2,2],
 id: "College-Credit",
 quote: "Finally, I Can Get A Degree In Gender Studies!",
 desc: "Improves Unpaid Interns Productivity By 200%",
 show: ref(true), //keep
},
{
  price: 12750,
 url: "https://cdn-icons-png.flaticon.com/512/6978/6978255.png",
 effect: ["reduce",2,.8],
 id: "College-Credit",
 quote: "Great Way To Announce The Layoffs",
 desc: "Reduces Unpaid Interns Price By 200%",
 show: ref(true), //keep
},
{
  price: 400,
 url: "https://code.visualstudio.com/assets/branding/app-icon.png",
 effect: ["click",1.5],
 id: "Visual-Studio-Code",
 quote: "The Ultimate Tool For Coders",
 desc: "Increases Click Power By 50%",
 show: ref(true), //ke
},
{
  price: 700,
  url: "https://pngimg.com/d/pacifier_PNG49.png",
  effect: ["percent",0,1.5],
  id: "Pacifier",
  quote: "Perfect for Helping Freshmen Focus",
  desc: "Improves Freshmen Productivity by 100%",
  show: ref(true),
},
{
  price: 1,
 url: "https://3.files.edl.io/fd75/20/04/09/191319-2af8eea0-9bd2-4795-8791-640f550a5c8f.png",
 effect: ["reduce",0,0.75],
 id: "Discovery Program",
 quote: "Now With 10% Fresher Men!",
 desc: "Reduces Price of Freshmen by 25%",
 show: ref(true),
},
{
  price: 2000,
     url: "https://fortniteskins.net/wp-content/uploads/2021/11/battle-pass-tiers-icon.png",
     effect: ["percent",1,2],
     id: "Battle-Pass",
     quote: "I Hope Oleg Is Happy Now",
     desc: "Improves Redditors Producitivity By 100%",
     show: ref(true),
    },
    {
      price: 3500,
        url: "https://cdn-icons-png.flaticon.com/512/2756/2756588.png",
        effect: ["reduce",1,0.8],
        id: "Deodorant",
        quote: "Perfect For Freshening Up The Basement",
        desc: "Reduces Redditors Price By 20%",
        show: ref(true),
       },
       {
      price: 78400,
        url: "https://avatars.githubusercontent.com/u/46283609?s=280&v=4",
        effect: ["reduce",3,0.8],
        id: "Fireship",
        quote: "Cookie Clicker In 100 Seconds",
        desc: "Reduces Youtube Tutorials By 20%",
        show: ref(true),
       },
       {
      price: 275000,
        url: "https://www.iconshock.com/image/Beta/Networking/byte/",
        effect: ["percent",4,2],
        id: "More-Bytes",
        quote: "Needed To Create Stack Underflow",
        desc: "Increases Stack Overflow Productivity By 100%",
        show: ref(true),
       },
       {
      price: 9000000,
        url: "https://cdn-icons-png.flaticon.com/512/3593/3593510.png",
        effect: ["percent",5,2],
        id: "GPT5",
        quote: "Can't Wait For This To Be Outdated In 2 Years",
        desc: "Increases Chat-GPT Productivity By 100%",
        show: ref(true),
       },
       {
      price: 10000000,
        url: "https://cdn-icons-png.freepik.com/512/2244/2244586.png",
        effect: ["percent",6,2],
        id: "Pay-Raise",
        quote: "And You're Still Not Paying The Intern?",
        desc: "Increases Paid Intern Productivity By 100%",
        show: ref(true),
       },
       {
      price: 255555455,
        url: "https://selfdeterminationtheory.org/wp-content/uploads/2022/07/parenting.svg",
        effect: ["percent",7,2],
        id: "Parental-Validation",
        quote: "The College Tryhards Can Finally Rest",
        desc: "Increases IIT Graduates Productivity By 100%",
        show: ref(true),
       },
       {
      price: 3968000000,
        url: "https://cdn-icons-png.freepik.com/512/2597/2597032.png",
        effect: ["percent",8,2],
        id: "True-Gender-Equality",
        quote: "IDK You Beat The Game.Good Job",
        desc: "Increases IIT Graduates Productivity By 100%",
        show: ref(true),
       },
       {
      price: 3968000001,
        url: "https://i.imgur.com/WItwZfy.png",
        effect: ["percent",0,20000],
        id: "Noah-Abbas",
        quote: "Made The Earth (In Javascript)",
        desc: ":)",
        show: ref(true),
       },
       {
      price: 3968000001,
        url: "https://i.imgur.com/UXck9Dj.png",
        effect: ["global",500],
        id: "Labe-Giberov",
        quote: "Proclaimed As The King Of Fortnite",
        desc: "(:",
        show: ref(true),
       },
       {
      price: 3968000001,
        url: "https://i.imgur.com/W01ZNNy.png",
        effect: ["click",40000],
        id: "Izzy-Zoltan",
        quote: "Something Funny IDK",
        desc: "._.",
        show: ref(true),
       },
]

upInfo.sort(compareObject)

console.log(upInfo)

function compareObject(a, b) {
  return a.price - b.price;
}

let goals = ref([
  {
title: "Hello World",
desc: "Get Your First Prestige",
p1: lifetime,
p2: 1,
rank: "common",
},
{
title: "You're Still Here?",
desc: "Get 100 Prestige",
p1: lifetime,
p2: 100,
rank: "common",
},
{
title: "Just Go Play Cookie Clicker",
desc: "Get 1,000 Prestige",
p1: lifetime,
p2: 1000,
rank: "uncommon",
},
{
title: "You Could Be Doing Something Else",
desc: "Get 10,000 Prestige",
p1: lifetime,
p2: 10000,
rank: "uncommon",
},
{
title: "What Do You Want?",
desc: "Get 100,000 Prestige",
p1: lifetime,
p2: 100000,
rank: "uncommon",
},
{
title: "Just Play An Actually Good Game",
desc: "Get 1,000,000 Prestige",
p1: lifetime,
p2: 1000000,
rank: "rare",
},
{
title: "dude...",
desc: "Get 10,000,000 Prestige",
p1: lifetime,
p2: 10000000,
rank: "rare",
},
{
title: "If You've Gotten Here Go Play Outer Wilds",
desc: "Get 100,000,000 Prestige",
p1: lifetime,
p2: 1000000000,
rank: "rare",
},
{
title: "It's A Start",
desc: "Hire A Freshmen",
p1: array[0].amount,
p2: 1,
rank: "common",
},
{
title: "Full Class",
desc: "Hire 25 Freshmen",
p1: array[0].amount,
p2: 25,
rank: "common",
},
{
title: "Why Do You Have So Many Children",
desc: "Hire 50 Freshmen",
p1: array[0].amount,
p2: 50,
rank: "common",
},
{
title: "Literally Just Child Labor",
desc: "Hire 100 Freshmen",
p1: array[0].amount,
p2: 100,
rank: "common",
},
{
title: `"So There's This Thing Called Bitcoin..."`,
desc: "Hire A Redditor",
p1: array[1].amount,
p2: 1,
rank: "common",
},
{
title: `8,000,000 Karma, 0 Girlfriends`,
desc: "Hire 25 Redditors",
p1: array[1].amount,
p2: 25,
rank: "common",
},
{
title: `JUST PAY THE POOR CHILD MONEY`,
desc: "Hire An Unpaid Intern",
p1: array[2].amount,
p2: 1,
rank: "common",
},
{
title: `https://www.youtube.com/watch?v=ipL7mEQJc4s`, 
desc: "Hire A Youtube Tutorial",
p1: array[3].amount,
p2: 1,
rank: "common",
},
{
title: `let NoahMixtape = 'fire'`,
desc: "Play A Song",
p1: startedMusic,
p2: true,
rank: "common",
},
])
array.push()
let displayText = ref([{name: "test", desc: "test", price: "test", quote: "test", hover: false}])
setInterval(prestigeAdd, 10);


function infoUpdate(details){
  displayText.value = [{name: details.id.replaceAll("-"," "), desc: details.desc, price: details.price + "Ᵽ", quote: details.quote, hover:true}]
}

function multAdd(plus){
  if(prestige.value >= plus.price){
    team.value++
    if(array[plus.index-1].amount.value == 0){
    array[plus.index-1].newUps.forEach(up => {
      upInfo[up].show.value = true
    })
  }
    array[plus.index-1].amount.value++
    prestige.value = prestige.value - plus.price
    multiChange()
    if(array[plus.index-1].price == 0){
      array[plus.index-1].price = array[plus.index-1].og
    }
    else{

      array[plus.index-1].price = array[plus.index-1].og * (1.15 ** (array[plus.index-1].amount.value))
    }
    array[plus.index-1].discounts.forEach(discount => {
      array[plus.index-1].price = array[plus.index-1].price * discount
    })
    array[plus.index-1].price = Math.floor(array[plus.index-1].price)
}
}



function multiChange(){
  multiplier.value = 0
  click.value = 1 + Math.floor(team.value/8)
  clickMulti.forEach(multi => {
    click.value = click.value * multi
  })
  click.value = Math.round(click.value)
  array.forEach(building =>{
    let indvValue = (building.value * building.amount.value)
    building.multipliers.forEach(multi =>{
      indvValue = indvValue * multi
    })
    multiplier.value = multiplier.value + indvValue
  })
}

function prestigeAdd(){
  // console.log(document.getElementById("upgrades"))
  prestige.value = prestige.value + multiplier.value
  lifetime.value = lifetime.value + multiplier.value
  return prestige
}
//https://i.imgur.com/YJBbqex.png 
function upAdd(details){
  if(prestige.value >= details.price){
    displayText.value[0].hover = false
    document.getElementById(details.id).remove()
    prestige.value = prestige.value - details.price
   if(details.effect[0] === "percent"){
    array[details.effect[1]].multipliers.push(details.effect[2])
   }
   if(details.effect[0] === "reduce"){
    array[details.effect[1]].discounts.push(details.effect[2])
    if(array[details.effect[1]].amount.value == 0){
      array[details.effect[1]].price = array[details.effect[1]].og 
    }
    else{
      array[details.effect[1]].price = (array[details.effect[1]].og * (1.15 ** (array[details.effect[1]].amount.value)))
    }
    array[details.effect[1]].discounts.forEach(discount => {
      array[details.effect[1]].price = array[details.effect[1]].price * discount
    })
    array[details.effect[1]].price = Math.floor(array[details.effect[1]].price)

   }
   if(details.effect[0] === "click"){
    clickMulti.push(details.effect[1])
   }
   multiChange()
  }
}


let audio = [
{
url: `https://ia800707.us.archive.org/14/items/MirrorTempleMirrorMagicMix/Mirror%20Temple%20%28Mirror%20Magic%20Mix%29.mp3`,
  name: "Mirror Temple B-Sides (Celeste)",
},
  {
  url: `https://vgmsite.com/soundtracks/omori-original-soundtrack-2020/zcbybavmne/86.%20World%27s%20End%20Valentine.mp3`,
  name: "Worlds End Valentine (Omori)",
},
{
  url: `https://vgmsite.com/soundtracks/terraria-pc-gamerip/sbavpvqbex/57.%20Empress%20of%20Light.mp3`,
  name: "Empress Of Light (Terraria)",
},
{
  url: `https://vgmsite.com/soundtracks/pokemon-emerald-remastered-complete-original-soundtrack/auhmjnziwh/3-14%20-%20Battle%21%20Frontier%20Brain%20%28Hoenn%29.mp3`,
  name: "Battle! Frontier Brain (RSE)",
},
{
  url: `https://ia801504.us.archive.org/6/items/undertaleost_202004/Undertale%20-%20Lossless%20Soundtrack%20%28toby%20fox%29/toby%20fox%20-%20UNDERTALE%20Soundtrack%20-%2025%20Dating%20Start%21.mp3`,
  name: "Dating Start! (Undertale)",
},
{
  url: `https://dl.vgmdownloads.com/soundtracks/hollow-knight-original-soundtrack/fwqiwachvp/06.%20Hornet.mp3`,
  name: "Hornet (Hollow Knight)",
},


{
  url: `https://vgmsite.com/soundtracks/outer-wilds-original-soundtrack/wvbkunihok/04.%20Space.mp3`,
  name: "Space (Outer Wilds)",
},
{
  url: `https://dl.vgmdownloads.com/soundtracks/pok-mon-heartgold-pok-mon-soulsilver-greatest-sounds-2009/aeewnkgpap/1-22.%20Violet%20City.mp3`,
  name: "Violet City (HGSS)",
},
{
  url: `https://vgmsite.com/soundtracks/minecraft/lqtvgglkpt/2-21.%20Wait.mp3`,
  name: "Wait (Minecraft)",
},
{
  url: `https://epsilon.vgmsite.com/soundtracks/portal/kpsfijlkjp/15.%20Still%20Alive%20%28Radio%20Mix%20Clean%29.mp3`,
  name: "Radio (Portal)",
},

{
  url: ``,
  name: "Stop Music",
},

]
let sound
function audioPlay(song){
  if(sound != undefined){
    sound.pause()
  }
  if(song.url == ""){
    console.log('ea')
  }
  else{
   sound = new Audio(song.url)
      console.log(startedMusic.value)
      sound.play()
      sound.loop = true
      soundChange()
      }
}

function soundChange(){
  if(sound){
    sound.volume = document.getElementById("slider").value/100
    if(sound.volume > 0){
      startedMusic.value = true
    }
  }
}

function close(id){
 document.getElementById(id).remove()
}

function cheatCheck(){
  switch(document.getElementById('cForm').value.replaceAll(" ","".toLowerCase().replaceAll('-',""))) {
  case "whalen":
    document.getElementById('whalen').src = 'https://i.imgur.com/YJBbqex.png'
    break;
  case "marill":
    document.getElementById('whalen').src = 'https://www.serebii.net/scarletviolet/pokemon/new/183.png'
    break;
  case "lostreel":
    audioPlay(`https://epsilon.vgmsite.com/soundtracks/outer-wilds-echoes-of-the-eye-the-lost-reels-deluxe-original-game-soundtrack-2022/tydjpboxwl/26.%20River%27s%20End%20Times.mp3`)
    break;
  case "noahabbasiq":
    prestige.value = Infinity 
    break;
  case "notnoahabbasiq":
    prestige.value = 0 
    break;
}   
}
</script>




<template>
  <div id="gal">
    <Notification :goals="goals" @close="(id) => close(id)"></Notification>
    <div id="lback">
    <div id="left">
<ArmyGalVue v-for="i in array.length" :key="i-1" :i="Object.assign(array[i - 1],{index: i})" :ref="prestige" :q="i[1]" @add="(i) => multAdd(i)"></ArmyGalVue>
    </div>
  </div>
  <div id="mid">
    <div id="cookie">
    <h1 id="count">Prestige: <span class="yText">{{ Math.round(prestige) }}</span></h1>
    <h3 id="stronk">Code Per Second = <span class="yText">{{ Math.round(multiplier * 10000)/100 }}</span></h3>
    
    <!--//https://i.imgur.com/YJBbqex.png stack https://upload.wikimedia.org/wikipedia/commons/e/ef/Stack_Overflow_icon.svg-->
  <img id="whalen" @click='prestige = prestige + click; lifetime = lifetime + click' src="https://upload.wikimedia.org/wikipedia/commons/e/ef/Stack_Overflow_icon.svg" alt="games broken xd" />
</div>
<UpInfo :display="displayText"></upInfo>
<div id="upgrades">
<BuffCard v-for="i in upInfo.length" :key="i-1" :info="upInfo[i - 1]" :id=upInfo[i-1].id  @defaultmenu="displayText[0].hover = false"  @display="(details) => infoUpdate(details)" @buy="(details) => upAdd(details)"></BuffCard>
</div>
</div>
<div id="rback">
  <div id="topr">
    <NavBar v-for="i in tabs" :tab="i" :test="prestige" @switch="(i) => mode = i"></NavBar>
  </div>
    <div id="right">  
  <OptionsTab  v-if="mode === 'options'" :audio="audio" @music="(i) => audioPlay(i)" @volume="soundChange(i)" @cheat="cheatCheck()" :stats="[{lifetime: lifetime, PPS: Math.round(multiplier * 10000)/100, team: team, power: click}]" ></OptionsTab>
      <AchievementTab  v-if="mode === 'achievements'" :goals="goals"></AchievementTab>
    </div>
  </div>
</div>
</template>


<style>

#topr{
  align-items: center;
  display: flex;
  justify-content: space-evenly;
  height: 5%;
  background-color: #2f2a49;
  border: black 3px solid;
  border-left: black 6px solid;
}
#lback{
  background-color: black;
  width: 25%;
}
#left{
height: 100%;
overflow: auto;
}
#rback{
  background-color: black;
  width: 25%;
}
#right{
height: 95%;
overflow: auto;
background-color: #2f2a49;
border-left: 6px solid #000000;
}

.yText{
  color: #ffd11a;
}



#upleft{
  margin-left: 1%;
  overflow: auto;
  flex-direction: column;
  display: flex;
  width: 60%;
  text-align: left
}

#upright{
  margin-right: 1%;
  overflow: auto;
  display: flex;
  flex-direction: column;
  width: 40%;
  text-align: right;
}

#upgrades{
  overflow: auto;
  display: flex;
  flex-direction: row;
}


#stronk{
  color: white;
}

#gal{
  top: calc(0px);
  height: calc(100vh);
  width: 100vw;
  position: absolute;
  left: 0px;
  background-image: url(https://imgur.com/ca2Om5H);
}

:root{
  background-image: ur;;
}
#whalen:hover{
  transition: .4s;
  transform: scale(1.05);
}
#whalen:active {
  transform: scale(.95);
}

#whalen{
  height: auto;
  width: 50%;
  z-index: 1;
}
#cookie{
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 75%;
}
#upgrades{
  display: flex;
  border: 3px black solid;
  border-top: 0px black solid;
  height: 16%;
  background-color: #000000;
  z-index: 0;
}

.upintext{
  font-size: .75rem;
}

h2{
  font-size: 1.25rem;
}
.upgradeinfo{
  flex-direction: row;  
  display: flex;
  color: black;
  border: 3px black solid;
  border-top: 6px black solid;
  border-bottom: 0px black solid;
  height: 9%;
  background-color: brown;
}

#slay{
  color:cadetblue
}
#count{
  color: white;
  margin-bottom: 1%;
  margin-top: 7.5%;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 3rem;
}

#ignore{
  color: white;
}
#gal{
  display: flex;
  text-align: center;
}
#mid{
  flex-direction: column;
  display: flex;
  justify-content: center;
  width: 50%;
background-image: linear-gradient(#161130,#2f2a49);

}
</style>