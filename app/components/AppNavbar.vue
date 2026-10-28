<template>
    <!--Background Color will Change later-->
    <div class="navbar grid grid-cols-[1fr_auto_1fr] bg-black px-6 md:px-12"> 

        <!--FOR LOGO-->
        <div class="justify-self-start">
            <NuxtLink to="/" class="flex items-center gap-3">
                <img
                  src="/logo.png"
                  alt="Yesha's Logo"
                  class="h-30 w-30 object-contain"/>
            </NuxtLink>
        </div>

        <!--NAVBAR-->
        <div class="flex items-center gap-6">
            <NuxtLink to ="/"
            class="text-gray-300 transition-colors hover:text-violet-400">Home</NuxtLink>
            <NuxtLink to ="/about-me"
            class="text-gray-300 transition-colors hover:text-violet-400">About Me</NuxtLink>
            <NuxtLink to ="/tech-stack"
            class="text-gray-300 transition-colors hover:text-violet-400">Tech Stack</NuxtLink>
            <NuxtLink to ="/certificates"
            class="text-gray-300 transition-colors hover:text-violet-400">Certificates</NuxtLink>
        </div>
    </div>
</template>