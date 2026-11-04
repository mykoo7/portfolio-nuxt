<template>
    <section class="relative z-10 flex flex-col items-center min-h-[80vh] pb-12">

        <div class="text-center">
            <h1 class="text-5xl font-extrabold text-center text-rose-950">
                GitHub Developer Activity
            </h1>

            <p class="text-sm text-center text-rose-900 mt-3 pb-3">
                An overview of my recent public GitHub commits and developmnent activity.
            </p>
        </div>

        <GithubActivityDashboard /> <!--CALLING THE GITHUB ACTIVITY DASHBOARD COMPONENT-->

         <p class="text-sm text-center text-rose-900 mt-3 pb-3">
            The data shown is based from public repositories using the GitHub REST API.</p>
        
    <!--BUTTON TO GO BACK TO TECHSTACK PAGE-->
        <NuxtLink to="/tech-stack" class="btn bg-rose-900 text-white hover:bg-rose-950 border-none rounded-xl">
            Back to Tech Stack
        </NuxtLink>
    </section>
</template>

<!--PAGE TITLE-->
<script setup>
import GithubActivityDashboard from '~/components/GithubActivityDashboard.vue';

useHead({
    title: 'GitHub Activity | Yesha Opon'
})

useSeoMeta({
  title: 'GitHub Activity | Yesha Opon',
  ogTitle: 'GitHub Activity | Yesha Opon',
  description: 'An overview of my recent public GitHub commits and developmnent activity.',
  ogDescription: 'An overview of my recent public GitHub commits and developmnent activity.',
  ogImage: '/images/index/opon-profile.jpg',
  twitterCard: 'summary_large_image',
})
</script>