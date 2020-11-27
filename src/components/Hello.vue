<template>
  <div class="hello">
    <nav id="menu">
      <div>
        <h1>teko toko</h1>
        <button class="overall-button" @click="clearEverything()">CLEAR</button>
      </div>
    </nav>

    <main id="panel">
      <header>
        <div><button class="toggle-button">☰</button></div>
        <div class="info" >
          <div class="entry" v-if="entry">ENTRY MODE</div>
          <div class="playing" v-else>PLAYING MODE</div>
        </div>
        <LetterEntry v-if="entry" @sendLetter="changeField($event)" class="LetterSelector" :changed=selectedSquare />
        <LetterSelector v-else @sendLetter="checkField($event)" class="LetterSelector" :changed=selectedSquare />

        <div class="vahe"></div>
        <button class="overall-button" @click="addField()">ADD FIELD</button>
        <div v-for="(field, idx) in fields" v-bind:key="idx">
          <div class="vahe"></div>
          <BingoField @changed="changed($event)" class="BingoField" :index=idx :field=field :atmSelected=atmSelected :correctSquares=correctSquares />
        </div>
        <div class="vahe"></div>
        <button class="overall-button" @click="changeMode()">CHANGE MODE</button>
        <div class="vahe"></div>
        <div class="vahe"></div>
        <div class="vahe"></div>

      </header>
    </main>
  </div>
</template>

<script>
import LetterEntry from "@/components/LetterEntry";
import LetterSelector from "@/components/LetterSelector";
import BingoField from "@/components/BingoField22";

function fieldInit(index) {
  let field = [];
  for (let i = 0; i < 5; i++) {
    field[i] = [];
    for (let j = 0; j < 5; j++) {
      field[i][j] = {
        fieldNr: index,
        value: null,
        x: i,
        y: j
      };
    }
  }
  return field;
}

function getFields() {
  let fields = JSON.parse(localStorage.getItem("gameFields"));
  if (fields == null) {
    return [];
  } else {
    return fields;
  }
}

function getCorrectSquares() {
  let guessedFields = JSON.parse(localStorage.getItem("guessedFields"));
  if (guessedFields == null) {
    return [];
  } else {
    return guessedFields;
  }
}


export default {
  name: 'hello',
  data () {
    return {
      selectedSquare: {
        fieldNr: -1,
        value: null,
        x: 0,
        y: 0
      },
      sendLetter: "",
      entry: true,
      fields: getFields(),
      correctSquares: getCorrectSquares(),
      atmSelected: 0
    }
  },
  components: {
    LetterEntry,
    LetterSelector,
    BingoField
  },
  methods: {
    changed : function(evento) {
      this.selectedSquare = evento;
      this.atmSelected = evento.fieldNr;
    },
    changeField: function(evento) {
      if (this.selectedSquare.fieldNr !== -1 && this.entry) {
        this.fields[this.selectedSquare.fieldNr][this.selectedSquare.x][this.selectedSquare.y].value = evento;
      }
      this.setCookies();
    },

    checkField: function(evento) {
      if (this.selectedSquare.fieldNr !== -1 && !this.entry) {
        let iterable = [...this.fields];
        iterable.reverse();
        let iterableLength = iterable.length;
        for (let i = 0; i < iterableLength; i++) {
          let field = iterable.pop();
          for (let j = 0; j < 5; j++) {
            for (let k = 0; k < 5; k++) {
              if (field[j][k].value === evento) {
                this.correctSquares.push(field[j][k]);
              }
            }
          }
        }
      }
      this.setCookies();
    },
    addField: function() {
      this.fields.push(fieldInit(this.fields.length));
    },
    changeMode: function() {
      this.entry = !this.entry;
    },
    clearEverything : function() {
      this.fields = [];
      this.correctSquares = [];
      this.setCookies();
    },
    setCookies: function() {
      localStorage.setItem("gameFields", JSON.stringify(this.fields));
      localStorage.setItem("guessedFields", JSON.stringify(this.correctSquares));
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

.overall-button {
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