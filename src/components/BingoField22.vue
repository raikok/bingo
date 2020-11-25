<template>
  <div>
    <div v-for="(column, idx) in field" :key="idx">
      <div v-for="(entry, idx2) in column" :key="idx2">
        <div class="selectedEntry" v-if="entry === selectedEntry && typeof(field[idx][idx2]) === 'object' "></div>
        <div class="selectedEntry" v-else-if="entry === selectedEntry && typeof(field[idx][idx2]) !== 'object' ">
          {{ field[idx][idx2] }}</div>
        <div class="unselectedEntry" v-else-if="typeof(field[idx][idx2])  === 'object' " @click="selectEntry(idx, idx2)"></div>
        <div class="unselectedEntry" v-else-if="typeof(field[idx][idx2])  !== 'object' " @click="selectEntry(idx, idx2)">
          {{ field[idx][idx2] }}</div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: "BingoField",
  data() {
    return {
      selectedEntryX: 0,
      selectedEntryY: 0,
      selectedEntry: null
    }
  },
  methods: {
    selectEntry : function(idx, idx2) {
      if (this.field[idx][idx2] == null) {
        console.log("selected = null");
      } else {
        this.$emit("changed");
        this.selectedEntryX = idx;
        this.selectedEntryY = idx2;
        this.selectedEntry = this.field[idx][idx2]
        let objekt = {
          fieldNr: 0,
          x: idx,
          y: idx2
        };
        this.$emit("changed", objekt);
      }
    }
  },
  props: {
    field: Array
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

</style>