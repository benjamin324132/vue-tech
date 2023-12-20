<template>
  <div class="subComment" :key="c" v-for="c in comments">
  <SubCommentCard :commentId="c" />
  </div>
</template>
<script>
import SubCommentCard from "@/components/SubCommentCard.vue";
export default {
  name: "SubCommentsList",
  props: {
    comments: Array
  },
  components:{
    SubCommentCard
  }
}
</script>

<style scoped>
  .subComment{
    padding-left: 30px;
  }
</style>
