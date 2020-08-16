<template>
  <div id="app">
    <Header />
    <div class="game-container">
      <Figure :wrongLetters="wrongLetters" />
      <WrongLetters :wrongLetters="wrongLetters" />
      <Word :selectedWord="selectedWord" :correctLetters="correctLetters" />
    </div>
    <Popup />
    <Notification v-if="showNotification" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Figure from "./components/Figure";
import WrongLetters from "./components/WrongLetters";
import Word from "./components/Word";
import Notification from "./components/Notification";
import Popup from "./components/Popup";

export default {
  name: "App",
  components: {
    Header,
    Figure,
    WrongLetters,
    Word,
    Notification,
    Popup,
  },
  data: function () {
    return {
      words: ["application", "programming", "interface", "wizard"],
      playable: true,
      correctLetters: [],
      wrongLetters: [],
      showNotification: false,
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
          } else {
            this.show();
          }
        } else {
          if (!this.wrongLetters.includes(letter)) {
            this.wrongLetters.push(letter);
          } else {
            this.show();
          }
        }
      }
    },
    show: function () {
      this.showNotification = true;
      setTimeout(() => {
        this.showNotification = false;
      }, 2000);
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
