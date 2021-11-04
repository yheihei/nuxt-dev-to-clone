<template>
  <div>
    <h3>Comments:</h3>
    <template v-if="comments.length > 0">
      <ul>
        <li v-for="(comment, index) in comments" :key="index">
          <div v-html="comment.body_html"></div>
          <div v-html="comment.user.name"></div>
        </li>
      </ul>
    </template>
    <template v-else>
      No comment...
    </template>
  </div>
</template>

<script>

export default {
  data() {
    return {
      comments: []
    }
  },
  async fetch() {
    this.comments = await fetch(
      `https://dev.to/api/comments?a_id=${this.$route.params.article}`
    ).then((res) => res.json())
    console.log(this.comments)
  },
  fetchOnServer: false
}
</script>