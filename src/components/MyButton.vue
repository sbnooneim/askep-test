<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'MyButton',
};
</script>

<style lang="scss" scoped>
.btn {
  padding: 12px 24px;
  border: 0;
  text-align: center;
  display: inline-block;
  transition: 0.3s;
  cursor: pointer;
  font-weight: 600;

  &:disabled {
    cursor: default;
    background-color: #ccc;
  }
}

.btn-primary {
  color: #fff;
  background-color: #14c1c5;
  border: 1px solid transparent;
  border-radius: 40px;

  &:not(:disabled):hover {
    background-color: #fff;
    color: #14c1c5;
    border-color: currentColor;
  }
}
.btn-secondary {
  color: #fff;
  background-color: #07567e;
  border: 1px solid transparent;
  border-radius: 40px;

  &:not(:disabled):hover {
    background-color: #fff;
    color: #07567e;
    border-color: currentColor;
  }
}
</style>
