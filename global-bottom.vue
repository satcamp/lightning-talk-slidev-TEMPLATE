<script setup lang="ts">
import { onBeforeUnmount, onMounted, watch, computed } from 'vue'
import { useNav } from '@slidev/client'

const SLIDE_MS = 15_000

// Disable auto-advance during development by opening the deck with `?noauto`
// in the URL, e.g. http://localhost:3030/?noauto — no file change needed.
const autoAdvance = !new URLSearchParams(window.location.search).has('noauto')

const { currentSlideNo, total } = useNav()

const overallScale = computed(() => currentSlideNo.value / total.value)

let timer: ReturnType<typeof setTimeout> | undefined

function schedule() {
  clearTimeout(timer)
  if (!autoAdvance || currentSlideNo.value >= total.value) return
  const next = currentSlideNo.value + 1
  // Use window.location.hash directly to avoid Slidev v52 embedding BASE_URL
  // into the hash fragment, which produces #/repo-name/2 (a 404 route).
  timer = setTimeout(() => { window.location.hash = '/' + next }, SLIDE_MS)
}

onMounted(schedule)
watch(currentSlideNo, schedule)
onBeforeUnmount(() => clearTimeout(timer))
</script>

<template>
  <div class="progress-bars">
    <!-- Countdown bar: right-to-left, resets each slide -->
    <div class="countdown-track">
      <div class="countdown-fill" :key="currentSlideNo" />
    </div>
    <!-- Overall progress: left-to-right -->
    <div class="overall-track">
      <div class="overall-fill" :style="{ transform: `scaleX(${overallScale})` }" />
    </div>
  </div>
</template>

<style scoped>
.progress-bars {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 100;
  pointer-events: none;
}

.countdown-track {
  height: 3px;
  background: rgba(9, 229, 123, 0.12);
  position: relative;
}

.countdown-fill {
  position: absolute;
  inset: 0;
  background: rgba(9, 229, 123, 0.55);
  transform-origin: right;
  animation: countdown-rtl 15s linear forwards;
}

@keyframes countdown-rtl {
  from { transform: scaleX(1); }
  to   { transform: scaleX(0); }
}

.overall-track {
  height: 4px;
  background: rgba(9, 229, 123, 0.12);
  position: relative;
}

.overall-fill {
  position: absolute;
  inset: 0;
  background: rgba(9, 229, 123, 0.55);
  transform-origin: left;
  transition: transform 0.3s ease;
}
</style>
