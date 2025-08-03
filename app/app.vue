<template>
  <div>
    <!-- <Header /> -->
    <NuxtPage />
  </div>
</template>

<script setup>
import Header from '@/components/header.vue'
definePageMeta({
  head: {
    link: [
      {
        rel: 'stylesheet',
        href: 'https://fonts.googleapis.com/css2?family=Moul&family=Siemreap&display=swap',
      },
    ],
  },
})

</script>
