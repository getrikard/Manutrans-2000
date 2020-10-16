<template>
  <div class="content">
    <h1>ManuTrans2000</h1>

    <!-- <p style="font-size: 1.125em">Putt inn din favorittutenlandske sangtekst og oversett i vei!</p> -->

    <!-- <div class="columns"> -->
      <div>
        <!-- <h2>Input</h2> -->
        <textarea id="text-input" @input="matrix()" placeholder="Putt inn din favorittutenlandske sangtekst og oversett i vei!"></textarea>
      </div>

      <!-- <div>
        <h2 style="text-align: right">Output</h2>
        <textarea
          id="text-input"
          @input="matrix()"
          :value="translatedText"
        ></textarea>
      </div> -->
    <!-- </div> -->

    <div class="matrix">
      <div class="line" v-for="(line, i) of outputText" :key="i">
        <div
          class="word"
          v-show="line != ''"
          v-for="(word, i) of line"
          :key="i"
        >
          <div v-show="word != ''">
            <input type="checkbox" name="" id="" />
            <a
              :href="'https://en.wiktionary.org/w/index.php?search=' + word"
              target="_BLANK"
            >
              {{ word }}
            </a>
          </div>

          <!-- <div>
            <input type="text" class="input-word" @input="translate()" />
          </div> -->
        </div>

        <div class="line blank" v-show="line == ''">
          <div class="word">
            <div>Ingenting</div>
            <!-- <div><input type="text" /></div> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Transition } from "vue";
export default {
  name: "App",
  data() {
    return {
      outputText: [],
      translatedText: "",
    };
  },
  methods: {
    matrix() {
      const textInput = document.getElementById("text-input");
      let matrix = [];

      for (const line of textInput.value.split("\n")) {
        const words = line.split(" ");
        let validWords = [];

        for (const word of words) {
          if (word == "") continue;
          validWords.push(word);
        }

        matrix.push(validWords);
      }

      this.outputText = matrix;
    },

    translate() {
      const wordInputs = [...document.getElementsByClassName("input-word")];
      let translation = "";

      for (const wordInput of wordInputs.filter((input) => input.value != "")) {
        translation += wordInput.value.trim() + " ";
      }

      this.translatedText = translation;
    },
  },
  mounted() {
    this.matrix();
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lobster&display=swap");
// @import url("https://fonts.googleapis.com/css2?family=Audiowide&display=swap");
// @import url("https://fonts.googleapis.com/css2?family=PT+Sans&display=swap");

// Colors:
$color1: #2f0024;
$color2: #70ffdf;
$color3: #ff7de9;
$color4: #fa16ab;

$font-family-header: "Lobster", sans-serif;
$font-family-normal: "PT Sans", Georgia, "Times New Roman", Times, serif;

%miami {
  background: linear-gradient(#ff7de9, #fa16ab);
  color: transparent;
  background-clip: text;
}

%common-input {
  box-sizing: border-box;
  width: 100%;
  background-color: rgba($color1, 0.85);
  color: white;
  border: 1px solid $color4;
  border-radius: 3px;
  padding: 0.5em;
  font-family: $font-family-normal;
  font-size: 1em;

  &:focus {
    box-shadow: 0 0 20px rgba($color2, 0.5);
  }
}

body {
  background-color: $color1;
  background-size: contain;
  background-attachment: fixed;
  font-family: $font-family-normal;
  // font-size: 1.125em;
  line-height: 1.5;
  color: $color4;
}

h1 {
  @extend %miami;

  font-family: $font-family-header;
  border-bottom: 4px solid rgba($color2, 0.85);
  border-bottom-left-radius: 2px;
  border-bottom-right-radius: 100%;
}

p {
  @extend %miami;

  max-width: 80ch;
  // margin: 1em auto;
}

a {
  color: $color2;
  text-decoration: none;
  border-bottom: 1px solid;

  &:hover {
    border-bottom: 0;
  }
}

textarea {
  @extend %common-input;

  resize: vertical;
  height: 50vh;
}

input[type="text"] {
  @extend %common-input;
}

input[type="checkbox"] {
  margin-right: 0.75em;
}

.content {
  max-width: 1024px;
  margin: auto;
}

.columns {
  display: flex;

  * {
    flex-grow: 1;
    flex-basis: 1;
  }

  & > :first-child {
    margin-right: 1em;
  }
}

.matrix {
  box-sizing: border-box;
  max-width: 1450px;
  margin: 3em auto;
  border: 1px solid $color4;
  border-radius: 3px;
  background-color: rgba($color1, 0.85);
}

.line {
  display: flex;
  margin: 1em 0;
  // border: 1px solid $color2;
  // padding: 0.5em;
}

.line.blank {
  visibility: hidden;
}

.word {
  text-align: center;
  margin-right: 0.5em;
  padding: 0.5em;
  min-width: 10px;
  border-radius: 3px;
  // font-size: 1.1em;
  letter-spacing: 0.125ch;
  color: $color2;

  & > :first-child {
    margin-bottom: 0.3em;
  }
}
</style>
