<template>
  <div class="card">
    <h3>{{ user }}</h3>
    <div class="comment" v-html="text">

    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "CommentCard",
  data() {
    return {
      user: "",
      text: "",
      subComments: []
    }
  },
  props: {
    commentId: String
  },
  methods: {
    async getComment() {
      const { data } = await axios.get(`https://hacker-news.firebaseio.com/v0/item/${this.commentId}.json?print=pretty`)
      console.log(data)
      this.text = data.text;
      this.user = data.by;
      if (data.kids) {
        this.subComments = data.kids
      }
    }
  },
  mounted() {
    this.getComment();
  }
}
</script>

<style scoped>
.card {
  padding: 12px 0;
}
.comment{
  font-size: 14px;
}
</style>
