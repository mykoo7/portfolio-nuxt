<!--PAGE TITLE-->
<script setup>
useHead({
  title: 'Tech Stack | Yesha Opon'
})
/* LINKED TO CERTFICATES COMPONENTS SO THAT IMAGE AND NAME WILL CHANGE */
const techCategories = [
  {
    title: 'Languages',
    items: [
      { name: 'Java', image: '/images/tech-stack/java.png' },
      { name: 'HTML', image: '/images/tech-stack/html.png' },
      { name: 'CSS', image: '/images/tech-stack/css.png' },
      { name: 'JavaScript', image: '/images/tech-stack/java-script.png' }
    ]
  },
  {
    title: 'Databases',
    items: [
      { name: 'PostgreSQL', image: '/images/tech-stack/postgresql.png' },
      { name: 'MongoDB', image: '/images/tech-stack/mongodb.png' }
    ]
  },
  {
    title: 'Tools',
    items: [
      { name: 'Git', image: '/images/tech-stack/git.png' },
      { name: 'GitHub', image: '/images/tech-stack/git-hub.png' },
      { name: 'VS Code', image: '/images/tech-stack/vscode.png' },
      { name: 'Android Studio', image: '/images/tech-stack/android-studio.png' }
    ]
  }
]
</script>

<template>
  <main class="relative z-10 flex flex-col items-center min-h-[80vh] pb-12">

    <!--PAGE HEADER-->
    <h1 class="text-5xl font-extrabold text-center text-rose-950">
      Tech Stack
    </h1>

    <!--TECH STACK FORMAT-->
    <div class="flex flex-col items-center gap-16 mt-8">

      <section
        v-for="category in techCategories"
        :key="category.title"
        class="flex flex-col items-center"
      >
        <h2 class="text-2xl text-center text-rose-950 font-extrabold">
          {{ category.title }}
        </h2>

        <div class="flex flex-wrap justify-center gap-8 px-10 pt-2 pb-4">
          <Techstack
            v-for="item in category.items"
            :key="item.name"
            :name="item.name"
            :image="item.image"
          />
        </div>
      </section>

    </div>

  </main>
</template>