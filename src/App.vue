<script setup>
import { ref } from "vue"
import mind from "./assets/mind.png"
const number = ref(null)
const show = ref(false)
const result = ref(false)
const messeges = ref(["Analyzing Brainwaves...","Scanning Memories...","Calculating Probabilities...","Decode Thoughts..."])
const currentMessege = ref("Analyzing Brainwaves...")
const div = ref()

const close = () => {
  show.value = !show.value
}

const starting = () =>{
let timer = 0 
let start = setInterval(()=>{
 if(timer < 20){
    currentMessege.value = messeges.value[0]
  }else if(timer < 40){
    currentMessege.value = messeges.value[1]
  }else if(timer < 60){
    currentMessege.value = messeges.value[2]
  }else if(timer < 80){
    currentMessege.value = messeges.value[3]
  }else if(timer > 100){
    currentMessege.value = messeges.value[4]
  }
  timer++
  div.value.style.cssText = `width: ${timer}%`
 
if(!show.value){
      clearInterval(start)
}
    if(timer === 100){
    clearInterval(start)
    result.value = true
    show.value = false
  }
},50)
}
const Caculate = () =>{
if(number.value > 10 || number.value < 1){
  return alert("Please enter a number between 1 and 10")
}
show.value = !show.value
return starting()
}
</script>

<template>
  <div class="flex min-h-screen items-center justify-center">
    <div class="bg-[#eee] w-[90%] sm:w-1/2 md:w-1/4 rounded overflow-hidden">
      <div class="flex bg-gray-300 p-3 gap-3">
        <img :src="mind" class="h-5 w-5" />
        <p class="font-semibold">Mind Reader</p>
      </div>
      <div class="p-3 text-center grid gap-4">
        <h1>Think Of Number Between 1 and 10</h1>
        <input
        v-model="number"
          type="number"
          class="w-1/2 text-center mx-auto"
          min="1"
          max="10"
        />

        <button @click="Caculate" class="w-fit mx-auto h-8 bg-gray-200 px-2">
          Read My Mind
        </button>
      </div>
    </div>
  </div>

  <div
    v-show="result"
    @click.self="result = false"
    class="bg-black bg-opacity-20 absolute w-screen h-screen top-0 flex justify-center items-center"
  >
    <Transition name="fade" appear>
      <div class="bg-[#eee] w-[90%] sm:w-1/2 md:w-1/4  rounded grid gap-5">
        <div class="flex bg-gray-300 p-3 gap-3">
          <img :src="mind" class="h-5 w-5" />
          <p class="font-semibold">Your Result is here!</p>
        </div>
        <h1 class="text-center font-semibold">The Number you're Thinking About is {{ number }} !!</h1>
         <div class="flex justify-end gap-3 mr-3 mb-3">
          <button class="h-8 bg-gray-300" @click="result = false">Close</button>
        </div>

      </div>
    </Transition>
  </div>



    <div
    v-show="show"
    @click.self="close"
    class="bg-black bg-opacity-20 absolute w-screen h-screen top-0 flex justify-center items-center"
  >
    <Transition name="fade" appear>
      <div class="bg-[#eee] w-[90%] sm:w-1/2 md:w-1/4  rounded grid gap-5">
        <div class="flex bg-gray-300 p-3 gap-3">
          <img :src="mind" class="h-5 w-5" />
          <p class="font-semibold">Reading Your Mind...</p>
        </div>
        <h1 class="text-center font-semibold">{{currentMessege}}</h1>
        <div class="w-[80%] h-5 p-1  bg-gray-300 border border-gray-400 mx-auto">
          <div ref="div" class=" h-full bg-green-500"></div>
        </div>
        
        <div class="flex justify-end gap-3 mr-3 mb-3">
          <button class="h-8 bg-gray-300" @click="close">Close</button>
        </div>
      </div>
    </Transition>
  </div>
</template>

<style>
button {
  background: silver;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #fff, inset -2px -2px grey,
    inset 2px 2px #dfdfdf;
  border: none;
  border-radius: 0;
  box-sizing: border-box;
  color: transparent;
  min-height: 23px;
  min-width: 75px;
  padding: 0 12px;
  text-shadow: 0 0 #222;
}
</style>
