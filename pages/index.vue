<template>
  <div class="page-wrapper">
    <div class="article-cards-wrapper">
      <article-card-block
        v-for="(article, i) in articles"
        :key="article.id"
        v-observe-visibility="
          i === articles.length - 1 ? lazyLoadArticles : false
        "
        :article="article"
        class="article-card-block"
      />
    </div>
  </div>
</template>

<script>
import ArticleCardBlock from '@/components/blocks/ArticleCardBlock'

export default {
  components: {
    ArticleCardBlock
  },
  data() {
    return {
      currentPage: 1,
      articles: []
    }
  },
  async fetch() {
    const articles = await fetch(
      `https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}`
    ).then(res => res.json())
    console.log(articles)
    this.articles = this.articles.concat(articles)
  },
  methods: {
    lazyLoadArticles(isVisible) {
      if (isVisible) {
        if (this.currentPage < 5) {
          this.currentPage++
          this.$fetch()
        }
      }
    }
  },
}
</script>
