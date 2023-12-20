<template>
  <div :key="c" v-for="c in comments">
   <CommentCard :comment-id="c" />
  </div>
</template>
<script>
import CommentCard from "@/components/CommentCard.vue"
export default {
  name: "CommentsList",
  props: {
    comments: Array
  },
  components:{
    CommentCard
  }
}
</script>
