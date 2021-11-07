<template>
  <div class="page-wrapper container">
    <template v-if="$fetchState.pending">
      <div class="article-cards-wrapper">
        <content-placeholders
          v-for="p in 30" :key="p"
          rounded
          class="article-card-block"
        >
          <content-placeholders-img />
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
    </template>
    <template v-else-if="$fetchState.error">
      <p>
        {{ $fetchState.error.message }}
      </p>
    </template>
    <template v-else>
      <div class="article-cards-wrapper">
        <article-card-block
          v-for="(article, i) in articles"
          :key="article.id"
          v-observe-visibility="
            i === articles.length - 1 ? lazyLoadArticles : false
          "
          :article="article"
        />
      </div>
    </template>
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
      `https://dev.to/api/articles?tag=nuxt&top=365&page=${this.currentPage}`
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

<style lang="scss" scoped>
.article-cards-wrapper {
  // padding: 5rem 0;
  display:grid;
  row-gap: 2rem;
  grid-template-columns: 1fr 1fr 1fr;
  column-gap: 2rem;
}
</style>