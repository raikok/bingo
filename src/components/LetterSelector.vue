<template>
  <div>
    <div class="selector">
      <div class="letters">
        <div v-for="letter in letters" v-bind:key="letter">
          <div class="selectedLetter" v-if="letter===selected">{{letter}}</div>
          <div class="unselectedLetter" v-else @click="selectLetter(letter)">{{letter}}</div>
        </div>

      </div>
      <input class="number" type="number">
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
  justify-content: center;

}

.number {
  width: 50%;
  display: inline-block;
  justify-content: center;
}

.selector {
  display:flex;
  flex-direction: column;
  flex-grow: 4;
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