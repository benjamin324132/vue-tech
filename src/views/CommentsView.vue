<template>
  <div class="container">
    <h2>{{ title }}</h2>
    <CommentsList :comments="comments" />
  </div>
</template>
<script>
import axios from "axios";
import CommentsList from "@/components/CommentsList.vue"
export default {
  name: "CommentsView",
  data() {
    return {
      title: "",
      comments: []
    }
  },
  methods:{
    async getPost(){
      const { data } = await axios.get(`https://hacker-news.firebaseio.com/v0/item/${this.$route.params.id}.json?print=pretty`);
      if(data.kids){
        this.comments = data.kids.slice(0, 10);
      }
      this.title = data.title
    }
  },
  components:{
    CommentsList
  },
  mounted(){
    this.getPost()
  }
}
</script>
<style scoped>
.container {
  max-width: 700px;
  margin: 0 auto;
}
</style>
