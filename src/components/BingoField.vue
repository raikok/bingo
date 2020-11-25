<template>
  <div>
    <div v-for="(column, idx) in field" :key="idx">
      <div v-for="(entry, idx2) in column" :key="idx2">
        <div class="selectedEntry" :item="letter" v-if="entry === selectedEntry">{{ letter }}</div>
        <div class="unselectedEntry" :item="letter" v-else @click="selectEntry(idx, idx2)">{{ letter }}</div>
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
        this.$emit("changed", true);
        this.selectedEntryX = idx2;
        this.selectedEntryY = idx;
        this.selectedEntry = this.field[idx][idx2]
      }
    }
  },
  props: {
    field: Array,
    letter: String
  }
}

</script>

<style scoped>

.selectedEntry {
  width: 10px;
  height: 10px;
  background-color: #bbe2ff;
  font-weight: 900;
  /*color: #ffffff;
  font-size: 250%;
  text-shadow: 4px 4px #777777;*/
}

.unselectedEntry {
  width: 10px;
  height: 10px;
  background-color: #000000;
  /*color: #6d6d6d;
  font-size: 250%;
  text-shadow: 4px 4px #000000;*/
}

</style>