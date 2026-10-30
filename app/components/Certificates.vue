
<script setup>
defineProps({
  name: {
    type: String,
    required: true
  },
  image: {
    type: String,
    required: true
  },
  verificationUrl: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['preview'])
</script>

<template>
  <div class="bg-rose-300 w-80 p-6 rounded-2xl shadow-md flex flex-col items-center text-center hover:-translate-y-1 hover:shadow-rose-950 hover:shadow-xl transition duration-300">

    <img
      :src="image"
      :alt="`${name} certificate`"
      class="w-70 h-50 object-cover rounded-xl mb-4 cursor-pointer"
      @click="emit('preview', image)"
    />

    <a
      :href="verificationUrl"
      target="_blank"
      rel="noopener noreferrer"
      class="text-rose-950 text-lg font-extrabold hover:underline"
    >
      {{ name }}
    </a>

  </div>
</template>
