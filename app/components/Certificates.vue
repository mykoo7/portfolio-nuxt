<!--PASSES INFO OF THE CERT NAME AND PIC AND LINK FROM THE CERT PAGE-->
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
<!--CERT CARD DESIGN-->
<template>
  <div class="bg-rose-100/20 backdrop-blur-sm
       border-2 border-rose-400/70
       w-80 p-6 rounded-2xl
       flex flex-col items-center text-center
       shadow-lg shadow-rose-950/30
       hover:bg-rose-100/30
       hover:border-rose-500
       hover:-translate-y-1
       hover:shadow-xl hover:shadow-rose-950/40
       transition duration-300">

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
