<template>
  <li class="comment-item">
    <p class="comment-author">{{ author }}</p>
    <p class="comment-text">{{ comment }}</p>
  </li>
</template>

<script>
export default {
  name: 'CommentItem',
  props: {
    comment: {
      type: String,
    },
    author: {
      type: String,
    },
  },

  setup() {},
};
</script>

<style scoped>
.comment-item {
  border: 1px solid #ccc;
  padding: 12px;
  margin-bottom: 10px;
}

.comment-author {
  font-weight: 700;
  font-size: 20px;
  margin-bottom: 8px;
}
</style>
