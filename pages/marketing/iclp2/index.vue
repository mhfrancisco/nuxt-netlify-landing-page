<template>
  <div class="post-page">
    <ThePostList :posts="posts" />
  </div>
</template>

<script>
import ThePostList from '~/components/templates/ThePostList'

export default {
  components: { ThePostList },
  async asyncData () {
    const mdFiles = await require.context('~/assets/content/landing-page/marketing/iclp2/', true, /\.md$/)
    return {
      posts: await mdFiles.keys().map(key => ({
        ...mdFiles(key),
        slug: `${key.replace('.md', '').replace('./', '')}`,
        path: 'iclp2'
      })).reverse()
    }
  }
}
</script>

<style scoped>
.post-page {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
