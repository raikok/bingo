<template>
  <div class="container">
    <button @click="undo()" class="overall-button">UNDO</button>
    <div class="history-text">History list:</div>
    <div class="letter" v-for="letter in guessedFields" :key="letter.value">
      {{letter.value}}
    </div>
  </div>
</template>

<script>

export default {
  name: "History",
  props: {
    guessedFields: Array
  },
  methods: {
    undo : function() {
      this.$emit("undoCorrect");
    }
  }
}
</script>

<style scoped>

  .history-text {
    margin-top: 25px;
    font-size: 25px;
    opacity: 100%;
    font-weight: bold;
    color: #222222;
    display: flex;
    justify-content: center;
    margin-bottom: 10px;
  }

  .letter{
    color: #222222;
    border-style: solid;
    border-width: thick;
    border-color: #222222;
    display: flex;
    justify-content: center;
  }
</style>