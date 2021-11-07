<template>
  <nuxt-link class="article-card-block" :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }" tag="article">
    <div class="article-card-block__image-wrapper">
      <img 
        v-if="article.cover_image"
        :src="article.cover_image"
        :alt="article.title"
        class="article-card-block__image"
      />
      <img v-else :src="article.social_image" :alt="article.title" class="article-card-block__image"/>
    </div>
    <div class="article-card-block__content">
      <nuxt-link :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }">
        <h1 class="article-card-block__title">{{ article.title }}</h1>
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
      <div class="article-card-block__meta">
        <div>
          <span class="article-card-block__meta_item">
            いいね
            {{ article.positive_reactions_count }}
          </span>
          <span class="article-card-block__meta_item">
            コメント
            {{ article.comments_count }}
          </span>
          <time class="article-card-block__meta_item">{{ article.readable_publish_date }}</time>
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

<style lang="scss" scoped>
.article-card-block {
  box-shadow: 2px 2px 8px $shadowColor;
  position: relative;
  padding-bottom: 2rem;

  &__image {
    width: 100%;
  }

  &__title {
    font-size: 2rem;
    text-decoration: none;
    padding-bottom: 1rem;
  }

  &__content {
    padding: 1rem;
  }

  &__meta {
    position: absolute;
    bottom: 1rem;
  }

  &__meta_item {
    padding-right: .5rem;
  }
}
</style>