<script setup>
defineProps({
  name: {
    type: String,
    required: true
  },
  image: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="flex flex-col items-center gap-3 hover:text-rose-950 transition duration-300">
    <img
      :src="image"
      :alt="`${name} logo`"
      class="w-24 h-24 object-contain rounded-xl shadow-md mix-blend-multiply"
    />

    <p class="text-lg text-rose-950 font-extrabold">
      {{ name }}
    </p>
  </div>
</template>