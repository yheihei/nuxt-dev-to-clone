<template>
  <section class="username-block">
    <img :src="user.profile_image" :alt="user.name" class="username-block__image">
    <div class="username-block__profile">
      <h1>{{ user.name }}</h1>
      <a
        :href="`https://dev.to/${user.username}`"
        target="_blank"
        class="btn btn-primary username-block__profile-follow mt-3">
        FOLLOW
      </a>
      <p v-if="user.summary" class="username-block__profile-summary mt-3 mb-0">{{ user.summary }}</p>
      <div class="username-block__sns-links mt-3">
        <a
          v-if="user.twitter_username"
          :href="`https://twitter.com/${user.twitter_username}`"
          target="_blank"
        >
          <twitter-icon />
        </a>
        <a
          v-if="user.github_username"
          :href="`https://github.com/${user.github_username}`"
          target="_blank"
        >
          <github-icon />
        </a>
        <a
        <a
          v-if="user.website_url"
          :href="user.website_url"
          target="_blank"
          rel="nofollow noopener noreferrer"
        >
          <external-link-icon />
        </a>
      </div>
    </div>
    <div class="username-block__meta">
      <div v-if="user.location">
        <div class="username-block__meta-title">location</div>
        <div class="username-block__meta-content">{{ user.location }}</div>
      </div>
      <div v-if="user.joined_at" class="mt-2">
        <div class="username-block__meta-title">joined</div>
        <div class="username-block__meta-content">{{ user.joined_at }}</div>
      </div>
    </div>
  </section>
</template>

<script>
import TwitterIcon from '~/assets/icons/twitter.svg?inline'
import GithubIcon from '~/assets/icons/github.svg?inline'
import ExternalLinkIcon from '~/assets/icons/external-link.svg?inline'

export default {
  components: {
    TwitterIcon,
    GithubIcon,
    ExternalLinkIcon
  },
  props: [],
  data() {
    return {
      user: {}
    }
  },
  async fetch() {
    const res = await fetch(
      `https://dev.to/api/users/by_username?url=${this.$route.params.username}`
    )
    if (!res.ok) {
      // set status code on server
      if (process.server) {
        this.$nuxt.context.res.statusCode = 404
      }
      throw new Error('User not found')
    }
    this.user = await res.json()
    console.log(this.user)
  }
}
</script>


<style lang="scss" scoped>
.username-block {
  display: flex;
  align-items: center;
  box-shadow: 2px 2px 8px $shadowColor;
  padding: 2rem;
  &__image {
    border-radius: 50%;
    width: 25%;
  }
  &__profile {
    padding: 0 2rem;
    width: 50%;
    &-follow {
      width: 100%;
      padding: .5rem;
    }
  }
  &__meta {
    width: 25%;
    &-title {
      color: gray;
    }
  }
}
</style>