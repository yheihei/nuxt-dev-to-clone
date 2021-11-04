<template>
  <article>
    <h1>
      {{ article.title }}
    </h1>
    <section v-html="article.body_html"></section>
  </article>
</template>

<script>

export default {
  data() {
    return {
      article: {
        type: Object,
        default: null
      }
    }
  },
  async fetch() {
    const article = await fetch(
      `https://dev.to/api/articles/${this.$route.params.article}`
    ).then((res) => res.json())
    // console.log(article)

    if (article.id && article.user.username === this.$route.params.username) {
      this.article = article
      this.$store.commit('SET_CURRENT_ARTICLE', this.article)
    }
  },
  activated() {
    if (this.$fetchState.timestamp <= Date.now() - 30000) {
      console.log('activated!!! re fetch!!!')
      this.$fetch()
    }
  }
}
</script>