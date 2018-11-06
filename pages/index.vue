<template>
  <v-layout
    row
    justify-center
    align-center>
    <h2>Blog</h2>
    <v-flex 
      v-for="post in posts" 
      :key="post.date"
      xs12
      sm8
      md6>
      <nuxt-link :to="post._path">
        {{ post.title }}
      </nuxt-link>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    // Using webpacks context to gather all files from a folder
    const context = require.context('~/content/blog/posts/', false, /\.json$/);

    const posts = context.keys().map(key => ({
      ...context(key),
      _path: `/blog/${key.replace('.json', '').replace('./', '')}`
    }));

    return { posts };
  }
}
</script>
