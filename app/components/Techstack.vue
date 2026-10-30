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
  <div class="flex flex-col items-center gap-2 hover:text-rose-950 transition duration-300">
    <img
      :src="image"
      :alt="`${name} logo`"
      class="w-20 h-20 object-contain rounded-xl shadow-md mix-blend-multiply"
    />

    <p class="text-rose-950 font-extrabold">
      {{ name }}
    </p>
  </div>
</template>