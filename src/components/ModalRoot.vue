<template>
  <div class="modal" v-show="isOpen">
    <div class="backdrop" @click="close"></div>
    <div class="modal-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalRoot',
  props: {
    isOpen: {
      type: Boolean,
      default: false,
    },
  },

  setup(_, ctx) {
    // console.log( ctx);
    const close = () => {
      ctx.emit('close');
    };

    return { close };
  },
  emits: ['close'],
};
</script>

<style scoped>
.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 30px;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 100;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal-content {
  position: relative;
  max-width: 750px;
  background-color: #fff;
  flex: 1;
  box-shadow: 0 0 1px 1px black;
  z-index: 100;
  overflow: hidden auto;
}
</style>
