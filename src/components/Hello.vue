<template>
  <div class="hello">
    <nav id="menu">
      <div>
        <h1>teko toko</h1>
      </div>
    </nav>

    <main id="panel">
      <header>
        <div><button class="toggle-button">☰</button>Panel</div>
        <LetterSelector class="LetterSelector"/>
      </header>
    </main>
  </div>
</template>

<script>
import LetterSelector from "@/components/LetterSelector";

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    LetterSelector
  }
}

</script>

<style>

.LetterSelector {
  display:flex;
  justify-content: center;
}

.toggle-button {
  margin-top: 1%;
  margin-left: 1%;
  width: 5%;
}
</style>