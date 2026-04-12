<template>
  <div style="display: flex; flex-direction: column; align-items: center; padding: 2rem 0;">
    <div style="height: 180px; display: flex; align-items: flex-end; gap: 1.2rem;">
      <div v-for="(bar, i) in bars" :key="i" style="display: flex; flex-direction: column; align-items: center;">
        <transition name="fade">
          <div v-if="step > i" :style="{
            width: '32px', height: bar.height + 'px', background: '#6497b1', borderRadius: '6px 6px 0 0', transition: 'height 0.5s', marginBottom: '0.5rem', boxShadow: '0 2px 8px #b3cde055'
          }"></div>
        </transition>
        <transition name="fade">
          <div v-if="step > i" :style="{ fontSize: '1.1rem', color: '#222', fontWeight: 'bold', minHeight: '1.5rem', marginTop: '0.2rem' }">
            {{ bar.word }}
          </div>
        </transition>
      </div>
    </div>
    <!-- No button, animation loops automatically -->
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const bars = [
  { word: 'the', height: 140 },
  { word: 'of', height: 100 },
  { word: 'and', height: 80 },
  { word: 'to', height: 60 },
  { word: 'a', height: 45 },
  { word: 'in', height: 35 },
  { word: 'is', height: 28 },
  { word: 'that', height: 22 },
  { word: 'it', height: 16 },
  { word: 'for', height: 12 },
  { word: 'pizza', height: 10 },
  { word: 'quokka', height: 2 },
]
const step = ref(0)
let interval = null
let timeout = null

function startLoop() {
  interval = setInterval(() => {
    if (step.value < bars.length) {
      step.value++
    } else {
      clearInterval(interval)
      timeout = setTimeout(() => {
        step.value = 0
        startLoop()
      }, 800)
    }
  }, 350)
}

onMounted(() => {
  startLoop()
})

onUnmounted(() => {
  clearInterval(interval)
  clearTimeout(timeout)
})
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
