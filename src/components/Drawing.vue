<template>
  <div class="drawing">
    <div class="picture">
      <img :src="`${publicPath}assets/${drawing.id}.jpg`" />
    </div>
    <div class="words">
      <word v-for="(word, index) in drawing.words" :key="index" :word="word" />
    </div>
  </div>
</template>

<script>
import Word from './Word.vue';

export default {
  name: 'Drawing',
  components: {
    Word,
  },
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
.drawing {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.picture {
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 20rem;
  flex-grow: 1;
}
.picture img {
  width: 100%;
}
</style>
