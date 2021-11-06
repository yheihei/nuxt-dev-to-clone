<template>
  <aside class="aside-username-block">
    <template v-if="user">
      <div>username: {{ user.name }}</div>
      <div v-if="user.twitter_username">twitter_username: @{{ user.twitter_username }}</div>
      <img :src="user.profile_image_90" :alt="user.name" width="90" height="90">
    </template>
  </aside>
</template>

<script>
export default {
  computed: {
    user() {
      const user = this.$store.state.currentArticle.user
      if (user) {
        return user;
      }
      else {
        return {}
      }
    }
  }
}
</script>