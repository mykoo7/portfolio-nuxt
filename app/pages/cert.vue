
<script setup>
import { ref } from 'vue'
/*PAGE TITLE*/
useHead({
  title: 'Certification | Yesha Opon'
})
/*LINKED TO CERTIFICATES COMPONENT AND LINKS TO VERIFICATION PAGE*/
const certificates = [
  {
    name: 'Microsoft Word Associate',
    image: '/images/certifications/ms-word-associate.jpg',
    verificationUrl: 'https://www.certiport.com/portal/pages/credentialverification.aspx'
  },
  {
    name: 'Microsoft PowerPoint Associate',
    image: '/images/certifications/ms-powerpoint-associate.jpg',
    verificationUrl: 'https://www.certiport.com/portal/pages/credentialverification.aspx'
  }
]

// CERT OPEN AND CLOSE
const isModalOpen = ref(false)
const selectedImage = ref('')

function openModal(image) {
  selectedImage.value = image
  isModalOpen.value = true
}

function closeModal() {
  isModalOpen.value = false
  selectedImage.value = ''
}
</script>

<template>
  <main class="relative z-10 flex flex-col items-center min-h-[80vh] pb-12">

    <h1 class="text-5xl font-extrabold text-center text-rose-950 mb-8">
      Certificates
    </h1>

    <section class="flex justify-center mt-5 mb-12 px-6">
      <div class="flex flex-wrap justify-center gap-6">

        <Certificates
          v-for="certificate in certificates"
          :key="certificate.name"
          :name="certificate.name"
          :image="certificate.image"
          :verification-url="certificate.verificationUrl"
          @preview="openModal"
/>

      </div>
    </section>

    <!--CERT DESIGN-->
    <div
      v-if="isModalOpen"
      class="fixed inset-0 bg-black/80 flex items-center justify-center z-50 cursor-pointer"
      @click="closeModal"
    >
      <img
        :src="selectedImage"
        alt="Certificate preview"
        class="max-w-[90%] max-h-[90%] rounded shadow-lg"
      />
    </div>

  </main>
</template>
