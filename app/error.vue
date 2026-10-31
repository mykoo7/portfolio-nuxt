<script setup>
defineProps({
    error: Object
})

const handleError = () => clearError({ redirect: '/' })
</script>

<template>
    <div class="min-h-screen relative flex flex-col items-center justify-center text-center">

        <!--ANIMATED COBWEB BACKGROUND-->
        <ErrorBackground />

        <!--404 INFO-->
        <div class="relative z-10 flex flex-col items-center">

            <p class="text-9xl font-bold text-rose-950">
                404
            </p>

            <p class="mt-3 text-3xl font-bold text-rose-950">
                You Have Wandered Too Far Away From Home
            </p>

            <!--404 LOGO-->
            <NuxtLink to="/" @click="handleError" class="mt-6">
                <img
                    src="/images/error/404-logo.png"
                    alt="Back to Home"
                    class="h-20 w-20 object-contain"
                />
            </NuxtLink>

            <!--BACK TO HOME BUTTON-->
            <button
                @click="handleError"
                class="mt-6 rounded-full border-2 border-rose-950 px-6 py-2
                       text-rose-950 hover:bg-rose-950 hover:text-white
                       transition duration-300"
            >
                Go Back Home
            </button>

        </div>
    </div>
</template>