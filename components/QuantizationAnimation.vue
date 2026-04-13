<template>
  <div style="display: flex; flex-direction: column; align-items: center; padding: 1.5rem 0;">
    <div style="display: flex; gap: 1.2rem; align-items: center; background: #e3eafc; border: 2px solid #b3cde0; border-radius: 12px; padding: 1.2rem 2rem; min-width: 320px;">
      <div v-for="(w, i) in weights" :key="i" :style="{
        width: '40px', height: '40px', borderRadius: '8px', display: 'flex', alignItems: 'center', justifyContent: 'center',
        background: quantized ? '#6497b1' : '#b3cde0', color: '#fff', fontWeight: 'bold', fontSize: '0.95rem', transition: 'background 0.3s'
      }">
        {{ quantized ? Math.round(w) : w.toFixed(2) }}
      </div>
    </div>
    <div style="color: #6497b1; font-size: 0.95rem; margin-top: 0.5rem;">Weight Vector</div>
    <div style="color: #888; font-size: 0.95rem;">Precision: {{ quantized ? 'int8' : 'float32' }}</div>
    <div style="color: #888; font-size: 0.9rem; margin-top: 0.5rem;">Quantization</div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const quantized = ref(false)
const weights = [1.23, -2.45, 0.98, 3.67, -1.11, 2.88]

const CYCLE_MS = 5000
const QUANTIZE_AT_MS = 2200
let cycleId
let phaseId

function runCycle() {
  quantized.value = false
  clearTimeout(phaseId)
  phaseId = setTimeout(() => {
    quantized.value = true
  }, QUANTIZE_AT_MS)
}

onMounted(() => {
  runCycle()
  cycleId = setInterval(runCycle, CYCLE_MS)
})

onBeforeUnmount(() => {
  clearInterval(cycleId)
  clearTimeout(phaseId)
})
</script>
