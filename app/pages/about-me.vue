
<template>
  <main class="relative z-10 flex flex-col items-center min-h-[80vh] pb-12">

    <!-- PAGE TITLE -->
    <h1 class="text-5xl font-extrabold text-center text-rose-950 mb-12"
    style="margin-bottom: 30px;">
      About Me
    </h1>

    <!-- ABOUT ME INFORMATION -->
    <section class="flex flex-col items-center gap-5 max-w-2xl px-12">

      <!-- PERSONAL INFORMATION -->
      <div class="bg-rose-300 font-extrabold text-rose-950 rounded-2xl p-6 shadow-lg w-full max-w-md hover:-translate-y-1 hover:shadow-rose-950 transition duration-300">
        <p class="text-sm leading-relaxed text-center">
          I am a 2nd year college student studying Information Technology.
          Currently interested in designing GUI's for school activities and projects.
          Whenever I get free time, I like to spend my time in reading fanfictions,
          watching movies, playing games on my laptop, and listening to music all day long.
          When things get tuff I always try to look on the bright side and keep up a positive attitude.
          Ofcourse food and drinks always gets me motivated.
        </p>
      </div>

      <!-- PROFESSIONAL ASPIRATIONS -->
      <div class="bg-rose-200 text-rose-950 font-extrabold rounded-2xl p-6 shadow-lg w-full max-w-md hover:-translate-y-1 hover:shadow-rose-950 transition duration-300">
        <p class="text-sm leading-relaxed text-center">
          My professional aspirations are centered on becoming a skilled front-end developer who build clean and responsive designs for websites.
          I aim to continuously hone my skills in html, css, javascript, and java.
          I would also like to work on my designing skills, picking the right colors, fonts, and designs to include in my next projects.
          I will also aim to be a full-stack developer when the time comes.
        </p>
      </div>

    </section>

  </main>
</template>

<script setup>
useHead({
  title: 'About | Yesha Opon'
})
</script>
