<template>
    <section class="relative z-10 flex flex-col items-center min-h-[80vh] pb-12">

        <div class="text-center">
            <h1 class="text-5xl font-extrabold text-center text-rose-950">
                Skills Dashboard
            </h1>
        <SkillsEcharts /> 
        </div>

         <p class="text-sm text-center text-rose-900 mt-3 pb-3">
        The scores reflect my own assessment of how familiar I am with each technology and are not based on formal testing.</p>
        
    <!--BUTTON TO GO BACK TO TECHSTACK PAGE-->
        <NuxtLink to="/tech-stack" class="btn bg-rose-900 text-white hover:bg-rose-950 border-none rounded-xl">
            Back to Tech Stack
        </NuxtLink>
    </section>
</template>

<!--PAGE TITLE-->
<script setup>
useHead({
    title: 'Skills Dashboard | Yesha Opon'
})

useSeoMeta({
  title: 'Skills Dashboard | Yesha Opon',
  ogTitle: 'Skills Dashboard | Yesha Opon',
  description: 'Skills knowledge percentage ranked Yesha Opon.',
  ogDescription: 'Skills knowledge percentage ranked Yesha Opon.',
  ogImage: '/images/index/opon-profile.jpg',
  twitterCard: 'summary_large_image',
})
</script>