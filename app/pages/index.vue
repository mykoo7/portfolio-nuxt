
<template>
    <!--HOMEPAGE FORMAT-->
    <section class="relative z-10 flex flex-col justify-center items-center px-6 sm:px-10 md:px-12 py-12 md:py-16 min-h-screen text-center gap-8 md:gap-10">

      <!--MY IMAGE-->
      <div class="w-40 h-40 sm:w-52 sm:h-52 md:w-60 md:h-60 rounded-full overflow-hidden border-4 border-rose-900">
        <img
          src="/images/index/opon-profile.jpg"
          alt="Yesha's Profile"
          class="w-full h-full object-cover"
        />
      </div>

      <!--INTRODUCTION-->
      <div class="max-w-lg">
        <h1 class="text-2xl sm:text-3xl md:text-4xl mb-4 text-rose-950 font-extrabold">
          Hi, I'm Ma. Yesha Klarisse Opon
        </h1>

        <p class="text-lg sm:text-xl text-rose-950">
          Aspiring front-end developer and student
        </p>

        <p class="text-lg sm:text-xl text-rose-900 font-extrabold pt-6">
          Contact Me
        </p>

        <!--GITHUB-->
        <a
          href="https://github.com/mykoo7"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-block"
        >
          <img
            src="/images/index/github.png"
            alt="GitHub"
            class="max-w-full h-auto rounded-lg hover:shadow-rose-950 hover:-translate-y-1 hover:shadow-xl transition duration-300 mix-blend-multiply"
          />
        </a>

        <!--LINKEDIN-->

        <a
          href="https://www.linkedin.com/in/mykoopon/"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-block"
        >
          <img
            src="/images/index/linkedin.png"
            alt="LinkedIn"
            class="max-w-full h-auto rounded-lg hover:shadow-rose-950 hover:-translate-y-1 hover:shadow-xl transition duration-300 mix-blend-multiply"
          />
        </a>
      </div>

    </section>
</template>

<!--PAGE TITLE-->
<script setup>
useHead({
  title: 'Home | Yesha Opon'
})
</script>
