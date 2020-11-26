<template>
  <div>
    <div v-for="(column, idx) in field" :key="idx">
      <div v-for="(entry, idx2) in column" :key="idx2">
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
      selectedEntry: null
    }
  },
  methods: {
    selectEntry : function(objekt) {
      console.log(this.correctSquares.includes(this.field[0][0]));
      console.log("------");
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

.selectedEntry {
  display:flex;
  justify-content: center;
  padding-top: 35%;
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

  width: 50px;
  height: 50px;
  background-color: #000000;
  color: #ffffff;
  font-size: 100%;
}

.correctEntry {
  display:flex;
  justify-content: center;
  padding-top: 35%;

  width: 50px;
  height: 50px;
  background-color: #ff0000;
  color: #ffffff;
  font-size: 100%;
}

</style>