<template>
  <div style="display: flex; flex-direction: column; align-items: center; padding: 1.5rem 0;">
    <div style="background: #e3eafc; border: 2px solid #b3cde0; border-radius: 12px; padding: 1.2rem 2rem; display: flex; gap: 1.2rem; align-items: center; min-width: 320px;">
      <div v-for="(head, i) in 6" :key="i" :style="{
        width: '32px', height: '32px', borderRadius: '50%', display: 'flex', alignItems: 'center', justifyContent: 'center',
        background: pruned && i === 2 ? '#e7f0f9' : '#6497b1', border: pruned && i === 2 ? '2px solid #b3cde0' : 'none', color: pruned && i === 2 ? '#888' : '#fff', fontWeight: 'bold', fontSize: '1rem', position: 'relative', transition: 'background 0.3s, color 0.3s'
      }">
        <span v-if="!(pruned && i === 2)">H{{i+1}}</span>
        <span v-else style="font-size: 1.3rem;">&#10005;</span>
      </div>
    </div>
    <div style="color: #6497b1; font-size: 0.95rem; margin-top: 0.5rem;">Transformer Block</div>
    <button @click="prune" style="margin-top: 1rem;">Prune</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const pruned = ref(false)
function prune() {
  pruned.value = true
}
</script>
