<template functional>
  <span class="word">
    {{
      props.word.solved
        ? props.word.word
        : props.word.word.replace(/[a-z]/g, '●')
    }}
  </span>
</template>

<script>
export default {
  name: 'Word',
};
</script>
