<script setup lang="ts">
import foodSource from './foods.json'

defineOptions({
  name: 'IndexPage',
})

const myLucky = ref()
const wheelState = reactive({
  blocks: [{ padding: '13px', background: '#ff6b6b' }],
  buttons: [{
    radius: '20%',
    background: '#ff6b6b',
    pointer: true,
    fonts: [{ text: '开始', top: '-10px' }],
  }],
})

const prizes = computed(() => {
  return foodSource.map((food: string, i: number) => {
    return {
      fonts: [{ text: food, top: '25%', fontSize: '14px' }],
      background: i % 2 === 0 ? '#fff5f5' : '#ffe3e3',
    }
  })
})

function startCallback() {
  myLucky.value.play()
  setTimeout(() => {
    const index = 0
    myLucky.value.stop(index)
  }, 3000)
}
</script>

<template>
  <div>
    <div text-4xl>
      <div i-carbon-campsite inline-block />
    </div>

    <button icon-btn @click="toggleDark()">
      <div i="carbon-sun dark:carbon-moon" />
    </button>

    <div m-t-6 flex justify="center">
      <LuckyWheel
        ref="myLucky" width="300px" height="300px" :prizes="prizes" :blocks="wheelState.blocks"
        :buttons="wheelState.buttons" @start="startCallback"
      />
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
