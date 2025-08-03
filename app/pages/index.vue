<template>
  <div
    class="min-h-screen flex flex-col items-center justify-center text-center px-4 relative overflow-hidden"
  >
    <!-- Background placeholder image with dark overlay -->
    <div
      class="absolute inset-0 bg-cover bg-center opacity-70"
      style="background-image: url('https://via.placeholder.com/1920x1080');"
      aria-hidden="true"
    ></div>
    <div class="absolute inset-0 bg-[#083f65] bg-opacity-60"></div>

    <!-- Content -->
    <div class="relative z-10 flex bg-white flex-col items-center border-2 shadow-xl border-gray-200 p-4 rounded-4xl text-black max-w-lg">
      <img
        src="/images/logo.png"
        alt="Logo"
        class="h-20 mb-6"
      />
      <h1 class="text-xl font-bold mb-2">
        ស្វាគតមកកាន់ការចុះឈ្មោះជាមន្ត្រី
      </h1>
        <h1 class="text-xl font-bold mb-2">
        ក្រសួងវេទមន្ត និងមន្តអាគម
      </h1>
      <p class="text-lg mb-6 font-bold">
            ចុះឈ្មោះដើម្បីបានកាតសំគាល់ខ្លួន      </p>
      <button
        @click="goToCardMaker"
        class="bg-[#083f65] text-white font-bold hover:bg-blue-900 px-6 py-2 rounded-lg transition"
      >
        ចាប់ផ្តើម
      </button>
    
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
const router = useRouter()

function goToCardMaker() {
  router.push('/cardmaker')
}
</script>

