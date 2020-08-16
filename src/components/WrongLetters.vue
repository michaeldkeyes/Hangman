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
.wrong-letters-container {
  position: absolute;
  top: 20px;
  right: 20px;
  display: flex;
  flex-direction: column;
  text-align: right;
}

.wrong-letters-container p {
  margin: 0 0 5px;
}

.wrong-letters-container span {
  font-size: 24px;
}
</style>