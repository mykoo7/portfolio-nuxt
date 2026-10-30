<script setup>
useHead({
  title: 'Tech Stack | Yesha Opon'
})

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
  <main class="relative z-10 flex flex-col justify-center min-h-screen py-12">

    <h1 class="text-5xl font-extrabold text-center text-rose-950">
      Tech Stack
    </h1>

    <section
      v-for="category in techCategories"
      :key="category.title"
      class="mt-12"
    >
      <h2 class="text-2xl text-center text-rose-950 font-extrabold">
        {{ category.title }}
      </h2>

      <div class="flex flex-wrap justify-center gap-6 px-10 py-4">
        <Techstack
          v-for="item in category.items"
          :key="item.name"
          :name="item.name"
          :image="item.image"
        />
      </div>
    </section>

  </main>
</template>