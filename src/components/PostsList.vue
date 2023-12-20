<template>
  <div :key="post" v-for="post in posts">
    <PostCard :post-id="post" />
  </div>
</template>

<script>
import PostCard from "./PostCard.vue"
export default {
  name: "PostsList",
  props:{
    posts: Array
  },
  components:{
    PostCard
  }
}
</script>
