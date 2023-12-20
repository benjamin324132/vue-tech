<template>
  <div class="container">
    <PostsList :posts="posts" />

    <v-btn @click="nextPage" variant="tonal">
      Load More
    </v-btn>
  </div>
</template>

<script lang="ts">
//  &limitToFirst=10&orderBy=%22$key%22
import axios from 'axios';
import PostsList from '@/components/PostsList.vue'
export default {
  name: "LayoutScreen",
  data() {
    return {
      totalPosts: [],
      posts: [],
      items: 10
    }
  },
  components: {
    PostsList
  },
  methods: {
    async getPosts() {
      const { data } = await axios.get("https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty");
      this.totalPosts = data
      this.posts = data.slice(0, 10)
    },
    nextPage() {
      this.items = this.items + 10;
      if (this.items < this.totalPosts.length)
        this.posts = this.totalPosts.slice(0, this.items)
      this.scrollToBottom()
    },
    scrollToBottom() {
      setTimeout(() => {
        window.scrollTo(0, document.body.scrollHeight || document.documentElement.scrollHeight);
      }, 1000)

    }
  },
  mounted() {
    this.getPosts()
  }
}

</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
}
</style>
