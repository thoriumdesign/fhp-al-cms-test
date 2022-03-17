<template>
  <main>
    <section v-if="post">
      <nav class="mb-8 max-w-3xl mx-auto">
        <nuxt-link to="/">
          <button class="
            bg-transparent 
            hover:bg-blue-800 
            text-blue-800 
            font-semibold 
            hover:text-white 
            py-2 
            px-4 
            border 
            border-blue-800 
            hover:border-transparent 
            rounded
            inline-flex
            items-center
          ">
            <svg class="fill-current w-4 h-4 mr-2" style="margin-left: -4px; margin-top: -2px;" viewBox="0 0 20 20">
              <path fill="currentColor" d="M15.41,16.58L10.83,12L15.41,7.41L14,6L8,12L14,18L15.41,16.58Z" />
            </svg>
            <span>Home</span></button>
        </nuxt-link>
      </nav>

      <article>
        <img
          v-if="post.cover"
          class="cover-image"
          :src="post.cover"
        >
        <!-- <h6 class="inline py-1 px-2 mr-1 bg-gray text-white text-sm font-medium rounded-sm">{{ post.category }}</h6> -->
        <h1 class="">{{ post.title }}</h1>
        <p class="mt-1 mb-8 text-primary-600 dark:text-primary-400">{{ post.description }}</p>
        <nuxt-content :document="post" />
        <div v-if="post.gallery" class="nuxt-content">
          <img
            v-for="image in post.gallery"
            class="image"
            :key="image.id"
            :src="image"
          >
        </div>
      </article>
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("entries", params.entry).fetch();
    } catch (e) {
      error({ message: "Entry not found" });
    }
    return { post };
  },
}
</script>
