<!--PASSES INFO OF THE TECHSTACK NAME AND PIC AND LINK FROM THE TECHSTACK PAGE-->
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
<!--TECHSTACK CARD DESIGN-->
<template>
  <div class="bg-rose-100/20 backdrop-blur-sm
         border-2 border-rose-400/70
         w-40 p-5 rounded-2xl
         flex flex-col items-center gap-3
         shadow-md shadow-rose-950/50
         hover:bg-rose-100/30
         hover:border-rose-300/80
         hover:-translate-y-1
         hover:shadow-lg hover:shadow-rose-950/100
         transition duration-300">
    <img
      :src="image"
      :alt="`${name} logo`"
      class="w-24 h-24 object-contain"
    />

    <p class="text-lg text-rose-950 font-extrabold">
      {{ name }}
    </p>
  </div>
</template>