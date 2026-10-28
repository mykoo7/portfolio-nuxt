<template>
    <div class="min-h-screen bg-black text-white">
        <div class="flex flex-col items-center pt-16 text-center">
            <p class="text-5xl font-bold">404</p>

            <p class="mt-3 text-xl">Page not found</p>

            <NuxtLink to="/" class="mt-6">
                <img
                src="/404-logo.png"
                alt="404 LOGO"
                class="j-20 w-20 object-contain"
                />
            </NuxtLink>
        </div>
    </div>
</template>