<template>
  <article>
    <template v-if="$fetchState.pending">
      <content-placeholders>
        <content-placeholders-heading></content-placeholders-heading>
        <content-placeholders-img></content-placeholders-img>
        <content-placeholders-text :lines="50"></content-placeholders-text>
      </content-placeholders>
    </template>
    <template v-else-if="$fetchState.error">
      <inline-error-block :error="$fetchState.error"></inline-error-block>
    </template>
    <template v-else>
      <h1>
        {{ article.title }}
      </h1>
      <section v-html="article.body_html" class="article-block__content"></section>
    </template>
  </article>
</template>

<script>

import InlineErrorBlock from '@/components/blocks/InlineErrorBlock'

export default {
  components: {
    InlineErrorBlock
  },
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
    } else {
      if (process.server) {
        this.$nuxt.context.res.statusCode = 404
      }
      throw new Error('Article not found')
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

<style lang="scss" scoped>
::v-deep .article-block__content {
  .ltag__user {
    display: none;
  }
  iframe {
    max-width: 100%;
  }
  h1 {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
  h2 {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
  h3 {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
  h4 {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
  p {
    margin-bottom: 1rem;
    line-height: 1.4;
    code {
      background-color: #d2f3e1;
      border-radius: 0.25rem;
      padding: 0.25rem;
    }
  }
  img {
    max-width: 100%;
    border-radius: 0.5rem;
  }
  .highlight {
    margin-bottom: 1rem;
    border-radius: 0.5rem;
  }
  ul {
    list-style: numeral;
    margin-bottom: 1rem;
    li p {
      margin-bottom: 0;
    }
  }
  ol {
    margin-bottom: 1rem;
  }
}
</style>