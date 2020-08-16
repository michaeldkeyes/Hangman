<template>
  <div id="app">
    <Header />
    <div class="game-container">
      <Figure :wrongLetters="wrongLetters" />
      <WrongLetters :wrongLetters="wrongLetters" />
      <Word :selectedWord="selectedWord" :correctLetters="correctLetters" />
    </div>
    <Popup
      v-if="status === 'win' || status === 'lose'"
      :finalMessage="finalMessage"
      :selectedWord="selectedWord"
      @playAgain="playAgain"
    />
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
      words: [
        "accurate",
        "bed",
        "camera",
        "deadly",
        "express",
        "formal",
        "gold",
        "hang",
        "import",
        "jump",
        "king",
        "ladder",
        "murder",
        "noble",
        "oak",
        "pluck",
        "quit",
        "ruin",
        "supply",
        "thoughtful",
        "use",
        "veil",
        "write",
        "xylophone",
        "youth",
        "zebra",
      ],
      playable: true,
      correctLetters: [],
      wrongLetters: [],
      showNotification: false,
      finalMessage: "",
      status: "",
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
            this.checkWin(
              this.correctLetters,
              this.wrongLetters,
              this.selectedWord
            );
          } else {
            this.show();
          }
        } else {
          if (!this.wrongLetters.includes(letter)) {
            this.wrongLetters.push(letter);
            this.checkWin(
              this.correctLetters,
              this.wrongLetters,
              this.selectedWord
            );
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
    checkWin: function (correct, wrong, word) {
      this.status = "win";
      this.finalMessage = "Congratulations! You won!";

      word.split("").forEach((letter) => {
        if (!correct.includes(letter)) {
          this.status = "";
          return;
        }
      });

      if (wrong.length === 6) {
        this.finalMessage = "Unfortunately you lost.";
        this.status = "lose";
        this.playable = false;
        return;
      }

      if (this.status === "win") {
        this.playable = false;
      }
    },
    playAgain: function () {
      this.playable = true;
      this.correctLetters = [];
      this.wrongLetters = [];
      this.status = "";

      // I didn't want to change selectedWord from a computed property so I made this janky workaround.
      let word = this.words.pop();
      this.words.push(word);
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
  width: 550px;
}

@media screen and (max-width: 750px) {
  .game-container {
    width: 450px;
  }
}

@media screen and (max-width: 400px) {
  .game-container {
    width: 350px;
  }
}
</style>
