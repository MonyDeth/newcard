<template>
  <div class="min-h-screen flex flex-col md:flex-row p-4 md:p-6 gap-6 bg-gray-50">
    <!-- Preview -->
  

    <!-- Edit Form (same as before) -->
    <div class="order-1 md:order-none w-full md:w-1/2 bg-white rounded-lg shadow p-6">
  <h2 class="text-2xl font-bold mb-6">កែប្រែព័ត៌មានកាត</h2>
  <form @submit.prevent="submitForm" class="space-y-6">
    <div>
      <label for="name" class="block font-medium mb-1">ឈ្មោះ</label>
      <input
        id="name"
        v-model="name"
        type="text"
        class="w-full border border-[#083f65] rounded-md px-4 py-2 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-900 focus:border-transparent"
        placeholder="បញ្ចូលឈ្មោះពេញ"
        required
      />
    </div>

    <div>
      <label for="position" class="block font-medium mb-1">មុខដំណែង</label>
      <input
        id="position"
        v-model="position"
        type="text"
        class="w-full border border-[#083f65] rounded-md px-4 py-2 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-900 focus:border-transparent"
        placeholder="បញ្ចូលមុខដំណែង"
        required
      />
    </div>

    <div>
      <label for="department" class="block font-medium mb-1">នាយកដ្ឋាន</label>
      <select
        id="department"
        v-model="department"
        class="w-full border border-[#083f65] rounded-md px-4 py-2 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-900 focus:border-transparent"
        required
      >
        <option disabled value="">ជ្រើសរើសអគ្គនាយកដ្ឋាន នាយកដ្ឋាន</option>
        <option>អគ្គនាយកដ្ឋាន ទស្សន៍ទាយ និងបង្ការគ្រោះ</option>
        <option>អគ្គនាយកដ្ឋាន វត្ថុទិព</option>
        <option>នាយកដ្ឋាន ទំនាក់ទំនង</option>
        <option>នាយកដ្ឋាន ប្រហាវេទមន្ត</option>
      </select>
    </div>

    <div>
      <label for="image" class="block font-medium mb-1">បញ្ចូលរូបភាព</label>
      <input
        id="image"
        type="file"
        @change="onImageChange"
        accept="image/*"
        class="w-full file:border-0 file:bg-blue-600 file:text-white file:px-4 file:py-2 file:rounded-md file:cursor-pointer hover:file:bg-blue-700 transition"
      />
    </div>


    <button
  type="submit"
  class="w-full bg-blue-600 text-white font-semibold py-3 rounded-md hover:bg-blue-700 transition flex items-center justify-center gap-2"
  :disabled="loading"
>
  <svg v-if="loading" class="animate-spin h-5 w-5 text-white" fill="none" viewBox="0 0 24 24">
    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" />
    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v4l3-3-3-3v4a8 8 0 00-8 8z" />
  </svg>
  <span>{{ loading ? 'កំពុងរក្សាទុក...' : 'រក្សាទុកកាត' }}</span>
</button>
  </form>
</div>


<div class="order-2 md:order-none w-full md:w-1/2 flex justify-center items-center">
            <div
            id="card-to-download"
            class="relative aspect-[2/3] w-full max-w-sm md:w-128 bg-white rounded-lg shadow-lg flex flex-col overflow-hidden bg-cover"
            style="background-image: url('/images/watermark.png')"
            >
        <!-- Top logo bar -->
        <div class="bg-[#083f65] h-18 flex items-center justify-center">
            <img src="/images/logo_long_white.png" alt="Logo" class="h-16 object-contain" />
        </div>

        <!-- Uploaded Image -->
        <div class="flex justify-center mt-8">
            <img
                v-if="imageUrl"
                :src="imageUrl"
                alt="Uploaded Image"
                class="w-24 h-32 scale-125 object-cover border-2 border-white shadow rounded"
            />
            <div
                v-else
                class="w-24 h-32 scale-125 bg-gray-300 border-2 border-white flex items-center justify-center text-gray-500 shadow rounded"
            >
                No Image
            </div>
            </div>


        <!-- Name -->
       <div class=" mt-8 text-center">
            <template v-if="hasKhmer(name) && hasLatin(name)">
                <div class="font-moul text-xl">{{ extractKhmer(name) }}</div>
                <div class="font-dm-serif text-lg mt-1">{{ extractLatin(name) }}</div>
            </template>
            <template v-else-if="hasKhmer(name)">
                <div class="font-moul text-xl">{{ name }}</div>
            </template>
            <template v-else>
                <div class="font-dm-serif text-xl font-semibold">{{ name || 'Full Name' }}</div>
            </template>
            </div>

        <!-- Position -->
        <div class="text-center flex mt-2 justify-center text-gray-700 mt-1 px-4 font-bold">
            <p class="me-1 font-siemreap text-base leading-snug">មុខដំណែង </p>
            <p class="ms-1 text-sm text-gray-500 font-dm-serif"> Position</p>
        </div>

        <p class="text-center text-2xl​ font-bold font-siemreap text-gray-700 mt-1 px-4">
          {{ position || 'មុខដំណែង' }}
        </p>
          <!-- Department -->
        <div class="text-center flex mt-2 justify-center text-gray-700 mt-1 px-4 font-bold">
            <p class="me-1 font-siemreap text-base leading-snug">នាយកដ្ឋាន </p>
            <p class="ms-1 text-sm text-gray-500 font-dm-serif"> Department</p>
        </div>

        <p class="text-center text-2xl​ font-bold font-siemreap text-gray-700 mt-1 px-4">
          {{ department || 'នាយកដ្ឋាន' }}
        </p>


        <!-- Effective Date -->
        <div class="text-center flex mt-auto justify-center text-gray-700 px-4 font-bold">
            <p class="me-1 font-siemreap text-base leading-snug">កាតធ្វើថ្ងៃទី</p>
            <p class="me-1 font-siemreap text-base leading-snug">Card Issue Date </p>
        </div>
        <p class="text-center text-xl font-dm-serif text-black">{{ today }}</p>



        <!-- Department bar -->
        <div
          :class="departmentBgColor(department)"
          class="mt-auto py-4 text-center text-white font-moul text-l"
        >
          {{ department || 'អគ្គនាយគដ្ឋាន នាយគដ្ឋាន ' }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import html2canvas from 'html2canvas'

const name = ref('')
const position = ref('')
const department = ref('')
const workingDate = ref('')

const imageUrl = ref(null)
const today = new Date().toLocaleDateString('en-GB', {
  year: 'numeric',
  month: 'long',
  day: 'numeric',
})

const loading = ref(false)
const imagePreview = ref(null)

async function submitForm() {
  loading.value = true

  try {
    const cardElement = document.querySelector('#card-to-download')
    const canvas = await html2canvas(cardElement, {
      scale: 2,
      useCORS: true,
    })

    const image = canvas.toDataURL('image/png')
    imagePreview.value = image

    // Optional: auto-download
    const link = document.createElement('a')
    link.download = `${name.value || 'card'}.png`
    link.href = image
    link.click()

  } catch (error) {
    alert('Something went wrong while generating the image.')
    console.error(error)
  }

  loading.value = false
}

function onImageChange(event) {
  const file = event.target.files[0]
  if (!file) {
    imageUrl.value = null
    return
  }
  imageUrl.value = URL.createObjectURL(file)
}


// Detect Khmer characters (Unicode range U+1780–U+17FF)
function isKhmer(text) {
  if (!text) return false
  return /[\u1780-\u17FF]/.test(text)
}

function formatDate(dateStr, locale = 'km-KH') {
  const options = { year: 'numeric', month: 'short', day: 'numeric' }
  return new Date(dateStr).toLocaleDateString(locale, options)
}

// Department background colors
function departmentBgColor(dep) {
  switch (dep) {
    case 'អគ្គនាយកដ្ឋាន ទស្សន៍ទាយ និងបង្ការគ្រោះ':
      return 'bg-red-600'
    case 'អគ្គនាយកដ្ឋាន វត្ថុទិព':
      return 'bg-green-600'
    case 'នាយកដ្ឋាន ទំនាក់ទំនង':
      return 'bg-blue-700'
    case 'នាយកដ្ឋាន ប្រហាវេទមន្ត':
      return 'bg-teal-700 text-gray-900'
    default:
      return 'bg-gray-700'
  }

}

function hasKhmer(text) {
  return /[\u1780-\u17FF]/.test(text);
}

function hasLatin(text) {
  return /[a-zA-Z]/.test(text);
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Moul&family=Siemreap&family=DM+Serif+Text&display=swap');

.font-moul {
  font-family: 'Moul', serif;
}

.font-siemreap {
  font-family: 'Siemreap', sans-serif;
}
.font-dm-serif {
  font-family: 'DM Serif Text', serif;
}
</style>

