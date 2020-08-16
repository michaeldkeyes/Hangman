<template>
  <div class="popup-container">
    <div class="popup">
      <h2>{{finalMessage}}</h2>
      <h3>{{finalMessageRevealWord}}</h3>
      <button @click="playAgain">Play Again</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    finalMessage: String,
    selectedWord: String,
  },
  computed: {
    finalMessageRevealWord() {
      return `... the word was: ${this.selectedWord}`;
    },
  },
  methods: {
    playAgain: function () {
      this.$emit("playAgain");
    },
  },
};
</script>

<style scoped>
.popup-container {
  background-color: rgba(0, 0, 0, 0.3);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup {
  background: #2980b9;
  border-radius: 5px;
  box-shadow: 0 15px 10px 3px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
}

.popup button {
  cursor: pointer;
  background-color: #fff;
  color: #2980b9;
  border: 0;
  margin-top: 20px;
  padding: 12px 20px;
  font-size: 16px;
}

.popup button:active {
  transform: scale(0.98);
}

.popup button:focus {
  outline: 0;
}
</style>