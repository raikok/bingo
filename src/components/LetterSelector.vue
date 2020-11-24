<template>
  <div>
    <div class="letters">
      <div class="letterBox" @click="selectLetter(letter)" v-for="letter in letters" v-bind:key="letter">
        <Letter letter>
        </Letter>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LetterSelector",
  data() {
    return {
      letters: ["B", "I", "N", "G", "O"],
      selected: null
    }
  },

  methods: {
    selectLetter : function (letter) {
      if (letter == null) {
        console.log("selected = null");
      } else {
        this.selected = letter;
        console.log("selected = " + letter);
      }
    }
  }
}
</script>

<style scoped>

.letters {
  display: flex;
  flex-direction: row;
}
.letterBox {
  color: #ffff;
  font-size: 250%;
}
</style>