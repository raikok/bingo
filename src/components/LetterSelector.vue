<template>
  <div>
    <div class="selector">
      <div class="letters">
        <div v-for="letter in letters" v-bind:key="letter">
          <div class="selectedLetter" v-if="letter===selectedLetter">{{letter}}</div>
          <div class="unselectedLetter" v-else @click="selectLetter(letter)">{{letter}}</div>
        </div>

      </div>
      <input id="number" pattern="[0-9]*" class="number" type="number">
      <div class="vahe"></div>
      <button class="button" @click="send">SEND</button>
      <span>{{this.answer}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "LetterSelector",
  data() {
    return {
      letters: ["B", "I", "N", "G", "O"],
      selectedLetter: null,
      selectedSquare: null,
      answer: null
    }
  },

  methods: {
    selectLetter : function (letter) {
      if (letter == null) {
        console.log("selected = null");
      } else {
        this.selectedLetter = letter;
      }
    },
    send : function() {
      if (this.selectedLetter === null || document.getElementById("number").value === 0) {
        alert("Vali ka äkki asjad");
      } else {
        let input = this.selectedLetter + document.getElementById("number").value;
        console.log(input);
        this.selectedLetter = null;
        this.answer = input;
        document.getElementById("number").value = '';
      }
    }
  }
}
</script>

<style scoped>

.letters {
  display: flex;
  flex-direction: row;
  justify-content: center;

}

.number {
  width: 27%;
  line-height: 3em;
  font-size: 200%;
  display: inline-block;
  justify-content: center;
  margin:auto;
  background-color: #6d6d6d;
  color: #bbe2ff;
  text-shadow: 4px 4px #777777;
}

.selector {
  display:flex;
  flex-direction: column;
}

.vahe {
  height: 10%;
}

.button {
  margin: auto;
  background-color: #6d6d6d;
  color: #000000;
  /*text-shadow: 4px 4px #000000;*/
  box-sizing: content-box;
  display: inline-block;
  height: 35px;
  width: 26%;
  border-width: 0;
}

.selectedLetter {
  font-weight: 900;
  color: #bbe2ff;
  font-size: 250%;
  text-shadow: 4px 4px #777777;
}

.unselectedLetter {
  color: #6d6d6d;
  font-size: 250%;
  text-shadow: 4px 4px #000000;
}
</style>