<template>
  <div class="entireField">
    <div class="vahe"></div>
    <div v-for="(column, idx) in field" class="field" :key="idx">
      <div v-for="(entry, idx2) in column" :key="idx2">
        <div v-if="idx === 0" class="letters">
          <div class="letter">{{letters[idx2]}}</div>
        </div>
        <div class="selectedEntry" v-if="entry === selectedEntry && atmSelected === index">
          {{ field[idx][idx2].value }}</div>
        <div class="correctEntry" v-else-if="correctSquares.includes(field[idx][idx2])">
          {{ field[idx][idx2].value }}
        </div>
        <div class="unselectedEntry" v-else @click="selectEntry(field[idx][idx2])">
          {{ field[idx][idx2].value }}</div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: "BingoField",
  data() {
    return {
      selectedEntry: null,
      letters: ["B", "I", "N", "G", "O"]
    }
  },
  methods: {
    selectEntry : function(objekt) {
      if (objekt === null) {
        console.log("selected = null");
      } else {
        this.selectedEntry = objekt;
        this.$emit("changed", objekt);
      }
    }
  },
  props: {
    index: Number,
    field: Array,
    atmSelected: Number,
    correctSquares: Array
  }
}

</script>

<style scoped>

.entireField {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.field {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.letters {
  color: #6d6d6d;
}

.selectedEntry {
  display:flex;
  justify-content: center;
  padding-top: 35%;

  border-style: solid;
  border-width: thin;
  border-color: #6d6d6d;
  width: 50px;
  height: 50px;
  background-color: #bbe2ff;
  font-weight: 900;
  color: #000000;
  font-size: 100%;

}

.unselectedEntry {

  display:flex;
  justify-content: center;
  padding-top: 35%;

  border-style: solid;
  border-width: thin;
  border-color: #6d6d6d;
  width: 50px;
  height: 50px;
  background-color: #212121;
  color: #ffffff;
  font-size: 100%;
}

.correctEntry {
  display:flex;
  justify-content: center;
  padding-top: 35%;

  border-style: solid;
  border-width: thin;
  width: 50px;
  height: 50px;
  background-color: #ff0000;
  color: #ffffff;
  font-size: 100%;
}

</style>