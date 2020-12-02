<template>
  <div>
    <div class="selector">
      <div class="vahe"></div>
      <input id="number" pattern="[0-9]*" class="number" type="number">
      <div class="vahe"></div>
      <button class="button" @click="send">SEND</button>
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
      selectedSquare: null
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
      if (document.getElementById("number").value === 0 || this.changed.fieldNr === -1) {
        alert("Sul on jäänud mõned lahtrid valimata (Number või lahter kuhu sisestad)");
      } else {
        let selectedLetter = "";
        switch (this.changed.y) {
          case 0:
            selectedLetter = "B";
            break;
          case 1:
            selectedLetter = "I";
            break;
          case 2:
            selectedLetter = "N";
            break;
          case 3:
            selectedLetter = "G";
            break;
          case 4:
            selectedLetter = "O";
            break;
        }
        let input = selectedLetter + document.getElementById("number").value;
        document.getElementById("number").value = '';
        this.$emit("sendLetter", input);
      }
    }
  },
  props: {
    changed: Object,
    entry: Boolean
  }
}
</script>

<style>

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

.button {
  margin: auto;
  background-color: #6d6d6d;
  color: #000000;
  /*text-shadow: 4px 4px #000000;*/
  box-sizing: content-box;
  display: inline-block;
  height: 20px;
  box-shadow: 1px 2px #888888;
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