<template>
  <aside class="aside-username-block">
    <template v-if="user">
      <div>username: {{ user.name }}</div>
      <div v-if="user.twitter_username">twitter_username: @{{ user.twitter_username }}</div>
      <img :src="user.profile_image" :alt="user.name" width="90" height="90">
    </template>
  </aside>
</template>

<script>
export default {
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