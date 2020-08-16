<template>
  <div id="app">
    <Header />
    <div class="game-container">
      <Figure :wrongLetters="wrongLetters" />
      <WrongLetters :wrongLetters="wrongLetters" />
      <Word :selectedWord="selectedWord" :correctLetters="correctLetters" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import Figure from "./components/Figure";
import WrongLetters from "./components/WrongLetters";
import Word from "./components/Word";

export default {
  name: "App",
  components: {
    Header,
    Figure,
    WrongLetters,
    Word,
  },
  data: function () {
    return {
      words: ["application", "programming", "interface", "wizard"],
      playable: true,
      correctLetters: [],
      wrongLetters: [],
    };
  },
  computed: {
    selectedWord: function () {
      return this.words[Math.floor(Math.random() * this.words.length)];
    },
  },
  methods: {
    handleKeydown: function (event) {
      const { key, keyCode } = event;
      if (this.playable && keyCode >= 65 && keyCode <= 90) {
        const letter = key.toLowerCase();

        if (this.selectedWord.includes(letter)) {
          if (!this.correctLetters.includes(letter)) {
            this.correctLetters.push(letter);
          }
        } else {
          if (!this.wrongLetters.includes(letter)) {
            this.wrongLetters.push(letter);
          }
        }
      }
    },
  },
  created: function () {
    window.addEventListener("keydown", this.handleKeydown);
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  background-color: #34495e;
  color: #fff;
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 80vh;
  margin: 0;
  overflow: hidden;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.game-container {
  display: flex;
  justify-content: space-around;
  padding: 20px 30px;
  position: relative;
  margin: auto;
  height: 350px;
  width: 450px;
}
</style>
