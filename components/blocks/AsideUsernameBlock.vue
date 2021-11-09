<template>
  <aside class="aside-username-block">
    <template v-if="user">
      <img :src="user.profile_image" :alt="user.name" width="90" height="90">
      <div class="mt-3">
        <nuxt-link :to="{
          name: 'username',
          params: { username: user.username }
        }">{{ user.name }}</nuxt-link>
      </div>
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
          v-if="user.website_url"
          :href="`${user.website_url}`"
          target="_blank"
        >
          <external-link-icon />
        </a>
      </div>
    </template>
  </aside>
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
      throw new Error(`User ${this.$route.params.username} not found`)
    }
    this.user = await res.json()
    console.log(this.user)
  }
}
</script>

<style lang="scss" scoped>
.aside-username-block {
  box-shadow: 2px 2px 8px $shadowColor;
  padding: 2rem;
}
</style>