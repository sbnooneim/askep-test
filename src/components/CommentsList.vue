<template>
  <h3 class="comments-title">Відгуки</h3>
  <ul class="comments-list" v-if="comments.length">
    <CommentItem
      v-for="comment in comments"
      :key="comment.id"
      :comment="comment.comment"
      :author="comment.author"
    />
  </ul>
  <p class="comments-empty" v-else>Відгуків поки немає, залишіть перший</p>
  <MyButton class="btn btn-primary" @click="loadMore" v-if="maxComments > maxCommentsToShow"
    >Завантажити ще</MyButton
  >
</template>

<script>
import CommentItem from './CommentItem.vue';
export default {
  name: 'CommentsList',
  components: { CommentItem },
  props: ['comments', 'loadMore', 'maxCommentsToShow', 'maxComments'],
  data() {
    return {};
  },
};
</script>

<style scoped>
.comments-title {
  font-size: 24px;
  padding: 20px;
}

.observe {
  height: 10px;
}
</style>
