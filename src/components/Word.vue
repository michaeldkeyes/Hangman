<template>
  <div class="word">
    <div v-for="(letter, index) in letters" :key="index">
      <span class="letter" v-if="correctLetters.includes(letter)">{{letter}}</span>
      <span class="letter" v-else></span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedWord: String,
    correctLetters: Array,
  },
  computed: {
    letters: function () {
      return this.selectedWord.split("");
    },
  },
};
</script>

<style scoped>
.word {
  display: flex;
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
}

.letter {
  border-bottom: 3px solid #2980b9;
  display: inline-flex;
  font-size: 30px;
  align-items: center;
  justify-content: center;
  margin: 0 3px;
  height: 50px;
  width: 20px;
}
</style>