<template>
  <div class="card">
     <router-link :to="getLink()">{{ post?.title }}</router-link>

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PostCard",
  data(){
  return {
    post: null
  }
  },
  props: {
    "postId": String
  },
  methods:{
    async getPost(){
      const { data } = await axios.get(`https://hacker-news.firebaseio.com/v0/item/${this.postId}.json?print=pretty`);
      this.post = data;
    },
    getLink(){
      return "/article/" + this.post?.id
    }
  },
  mounted(){
    this.getPost()
  }
}
</script>

<style scoped>
 .card{
  padding: 10px 0;
 }
</style>
