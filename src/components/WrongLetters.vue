<template>
  <div class="wrong-letters-container">
    <p>Wrong</p>
    <div class="d-flex" v-if="wrongLetters.length > 0">
      <span v-for="(letter, index) in wrongLetters" :key="index">
        <pre>{{letter}}, </pre>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    wrongLetters: Array,
  },
};
</script>

<style scoped>
.d-flex {
  display: flex;
  flex-wrap: wrap;
}
</style>