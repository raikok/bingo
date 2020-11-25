<template>
  <div class="hello">
    <nav id="menu">
      <div>
        <h1>teko toko</h1>
      </div>
    </nav>

    <main id="panel">
      <header>
        <div><button class="toggle-button">☰</button></div>
        <div class="info" >
          <info class="entry" v-if="entry">ENTRY MODE</info>
          <info class="playing" v-else>PLAYING MODE</info>
        </div>
        <LetterSelector @sendLetter="changeField($event)" class="LetterSelector" :changed=selectedSquare />
        <div class="vahe"></div>
        <BingoField @changed="changed($event)" class="BingoField" :field=field />
        <div class="vahe"></div>
        <button class="change-mode" @click="changeMode()">CHANGE MODE</button>
      </header>
    </main>
  </div>
</template>

<script>
import LetterSelector from "@/components/LetterSelector";
import BingoField from "@/components/BingoField22";

function fieldInit() {
  let field = [];
  for (let i = 0; i < 5; i++) {
    field[i] = [];
    for (let j = 0; j < 5; j++) {
      field[i][j] = {
        i: i,
        j: j
      };
    }
  }
  return field;
}

export default {
  name: 'hello',
  data () {
    return {
      selectedSquare: {
        fieldNr: -1,
        x: 0,
        y: 0
      },
      sendLetter: "",
      field: fieldInit(),
      entry: true
    }
  },
  components: {
    LetterSelector,
    BingoField
  },
  methods: {
    changed : function(evento) {
      this.selectedSquare = evento;
    },
    changeField: function(evento) {
      console.log("letter: " + evento);
      if (this.selectedSquare.fieldNr !== -1 && this.entry) {
        this.field[this.selectedSquare.x][this.selectedSquare.y] = evento;
      }
    },
    checkField: function(evento) {
      if (this.selectedSquare.fieldNr !== -1 && !this.entry) {
        this.field[this.selectedSquare.x][this.selectedSquare.y] = evento;
      }
    },
    changeMode: function() {
      this.entry = !this.entry;
    }
  }
}

</script>

<style>

.info {
  display: flex;
  justify-content: center;
  font-size: 75%;
}

.info .entry {
  color: #6d6d6d;
  text-shadow: 4px 4px #000000;
}

.info .playing {
  color: #bbe2ff;
  text-shadow: 1px 1px #777777;
}

.LetterSelector {
  display:flex;
  justify-content: center;
}

.BingoField {
  display:flex;
  justify-content: center;
}

.vahe {
  height: 10px;
}

.toggle-button {
  background-color: #6d6d6d;
  margin-top: 1%;
  margin-left: 1%;
  width: 5%;
}

.change-mode {
  display: flex;
  justify-content: center;
  margin: auto;
  background-color: #6d6d6d;
  color: #000000;
  /*text-shadow: 4px 4px #000000;*/
  box-sizing: content-box;
  height: 20px;
  box-shadow: 1px 2px #888888;
  width: 26%;
  border-width: 0;
}

</style>