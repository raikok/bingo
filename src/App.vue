<template>
  <div id="app">

    <Slideout :touch="false" :toggleSelectors="['.toggle-button', '.another-toggle']">
      <Hello/>
    </Slideout>
  </div>
</template>

<script>
import Slideout from "vue-slideout";
import Hello from "./components/Hello";

export default {
  name: "app",
  components: {
    Hello,
    Slideout
  },
  mounted: function() {
  },
  methods: {
  }
};
</script>
<style>
@import url(https://fonts.googleapis.com/css2?family=Roboto+Slab&display=swap);
* {
  font-family: 'Roboto Slab', serif;
  outline: none;
}
body {
  width: 100%;
  height: 100%;
  margin: 0;
}

.slideout-menu {
  position: fixed;
  top: 0;
  bottom: 0;
  width: 256px;
  height: 100%;
  /*overflow-y: scroll;*/
  -webkit-overflow-scrolling: touch;
  z-index: 0;
  display: none;
  background-color: #6d808c;
  color: white;
}

.slideout-menu-left {
  left: 0;
}

.slideout-menu-right {
  right: 0;
}

.slideout-panel {
  background-color: #212121;
  color: white;
  position: relative;
  z-index: 1;
  will-change: transform;
  min-height: 100vh;
}

.slideout-open,
.slideout-open body,
.slideout-open .slideout-panel {
  overflow: hidden;
}

.slideout-open .slideout-menu {
  display: block;
}
</style>
