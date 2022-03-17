<template>
  <main>
    <section v-if="posts" class="w-full max-w-2xl mx-auto">
      <h1 class="title">Applied Libertarianism Entries</h1>
      <posts post-type="entries" :amount="10" />
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, error }) {
    let posts;
    try {
      posts = await $content("entries").fetch();
    } catch (e) {
      error({ message: "Entries not found" });
    }
    return { posts };
  },
}
</script>
