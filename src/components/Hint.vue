<template>
  <div class="hint">
    <img :src="`${publicPath}assets/hint.jpg`" />
  </div>
</template>

<script>
export default {
  name: 'Hint',
  props: {
    drawing: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      publicPath: process.env.BASE_URL,
    };
  },
};
</script>

<style scoped>
img {
  max-width: 20rem;
}

.hint {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
