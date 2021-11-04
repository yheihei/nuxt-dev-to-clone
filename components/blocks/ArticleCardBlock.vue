<template>
  <nuxt-link :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }" tag="article">
    <div class="image-wrapper">
      <img 
        v-if="article.cover_image"
        :src="article.cover_image"
        :alt="article.title"
      />
      <img v-else :src="article.social_image" :alt="article.title"/>
    </div>
    <div class="content">
      <nuxt-link :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }">
        <h1>{{ article.title }}</h1>
      </nuxt-link>
      <div class="tags">
        <nuxt-link
          v-for="tag in article.tag_list" :key="tag"
          :to="{ name: 't-tag', params: { tag } }"
          class="tag"
        >
          #{{ tag }}
        </nuxt-link>
      </div>
      <div class="meta">
        <div class="scl">
          <span>
            いいね
            {{ article.positive_reactions_count }}
          </span>
          <span>
            コメント
            {{ article.comments_count }}
          </span>
          <time>{{ article.readable_publish_date }}</time>
        </div>
      </div>
    </div>
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

<style>
.image-wrapper img {
  width: 400px;
}
</style>