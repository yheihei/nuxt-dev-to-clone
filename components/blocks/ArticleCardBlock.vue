<template>
  <nuxt-link :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }">
    hoge
  </nuxt-link>
</template>

<script>
export default {
  props: {
    article: {
      type: Object,
      default: null
    }
  }
}
</script>