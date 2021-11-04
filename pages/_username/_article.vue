<template>
  <div class="page-wrapper">
    <div class="article-content-wrapper">
      <article-block class="article-block" />
      <aside-username-block class="aside-username-block"></aside-username-block>
    </div>
    <comments-block class="comments-block"></comments-block>
  </div>
</template>

<script>
  import ArticleBlock from '@/components/blocks/ArticleBlock'
  import CommentsBlock from '@/components/blocks/CommentsBlock'
  import AsideUsernameBlock from '@/components/blocks/AsideUsernameBlock'

  export default {
    components: {
      ArticleBlock,
      CommentsBlock,
      AsideUsernameBlock
    }
  }
</script>
