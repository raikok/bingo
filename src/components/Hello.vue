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
          <div class="entry" v-if="entry">ENTRY MODE</div>
          <div class="playing" v-else>PLAYING MODE</div>
        </div>
        <LetterSelector v-if="entry" @sendLetter="changeField($event)" class="LetterSelector" :changed=selectedSquare :entry=entry />
        <LetterSelector v-else @sendLetter="checkField($event)" class="LetterSelector" :changed=selectedSquare :entry=entry />

        <div class="vahe"></div>
        <button class="overall-button" @click="addField()">ADD FIELD</button>
        <div v-for="(field, idx) in fields" v-bind:key="idx">
          <div class="vahe"></div>
          <BingoField @changed="changed($event)" class="BingoField" :index=idx :field=field :atmSelected=atmSelected :correctSquares=correctSquares />
        </div>
        <div class="vahe"></div>
        <button class="overall-button" @click="changeMode()">CHANGE MODE</button>
      </header>
    </main>
  </div>
</template>

<script>
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
      fields: [],
      correctSquares: [],
      atmSelected: 0
    }
  },
  components: {
    LetterSelector,
    BingoField
  },
  methods: {
    changed : function(evento) {
      this.selectedSquare = evento;
      this.atmSelected = evento.fieldNr;
    },
    changeField: function(evento) {
      console.log("letter: " + evento);
      if (this.selectedSquare.fieldNr !== -1 && this.entry) {
        console.log("väljad: " + this.fields);
        console.log("selectedSquare: " + this.selectedSquare);
        this.fields[this.selectedSquare.fieldNr][this.selectedSquare.x][this.selectedSquare.y].value = evento;
      }
    },

    checkField: function(evento) {
      console.log("checking...");
      if (this.selectedSquare.fieldNr !== -1 && !this.entry) {
        let iterable = [...this.fields];
        iterable.reverse();
        let iterableLength = iterable.length;
        for (let i = 0; i < iterableLength; i++) {
          let field = iterable.pop();
          for (let j = 0; j < 5; j++) {
            for (let k = 0; k < 5; k++) {
              if (field[j][k].value === evento) {
                console.log("leidis kh");
                this.correctSquares.push(field[j][k]);
              }
            }
          }
        }
      }
    },
    addField: function() {
      console.log("adding field");
      this.fields.push(fieldInit(this.fields.length));
      console.log(this.fields);
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