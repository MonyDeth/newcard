<template>
  <div>
    <!-- Loading screen -->
    <div
      ref="loader"
      class="fixed inset-0 z-50 flex items-center justify-center overflow-hidden"
      style="background-color: #093E65"
    >
      <div class="text-center text-white">
        <img
          src="/images/logo.png"
          alt="Logo"
          class="w-40 mx-auto mb-4 flicker"
        />
        <div class="text-xl font-bold py-4">ចាំតិច មេ...</div>
      </div>
    </div>

    <!-- Actual page content -->
    <div ref="appContent">
      <NuxtPage />
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick, onMounted } from 'vue'
import { gsap } from 'gsap'

const loader = ref(null)
const appContent = ref(null)

onMounted(async () => {
  await nextTick()

  requestAnimationFrame(() => {
    setTimeout(() => {
      // Animate loader down with rounded top corners
      gsap.to(loader.value, {
        y: '100%',
        borderTopLeftRadius: '2000px',
        borderTopRightRadius: '2000px',
        duration: 0.8,
        ease: 'power3.in',
      })
    }, 1500)
  })
})
</script>

<style scoped>
.flicker {
  animation: flicker 1.2s infinite ease-in-out;
}

@keyframes flicker {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.6; }
}
</style>
