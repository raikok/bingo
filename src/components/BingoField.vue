<template>
  <div>
    <div v-for="column in field" :key="column">
      <div v-for="entry in column" :key="entry">
        <div class="selectedEntry" v-if="entry===selectedEntry">{{entry}}</div>
        <div class="unselectedEntry" v-else @click="selectEntry(entry)">{{entry}}</div>
      </div>
    </div>
  </div>
</template>

<script>
function fieldInit() {
  let field = [];
  for (let i = 0; i < 5; i++) {
    field[i] = [i];
  }
  return field;
}

export default {
  name: "BingoField",
  data() {
    return {
      field: fieldInit(),
      selectedEntry: null
    }
  },
  methods: {
    selectEntry : function(entry) {
      if (entry == null) {
        console.log("selected = null");
      } else {
        this.selectedEntry = entry;
        console.log(this.selectedEntry);
      }
    }
  }
}

</script>

<style scoped>

</style>