<template>
  <div id="app">
    <Header />
    <div class="game-container">
      <Figure />
      <WrongLetters />
      <Word />
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

.game-container {
  padding: 20px 30px;
  position: relative;
  margin: auto;
  height: 350px;
  width: 450px;
}
</style>
