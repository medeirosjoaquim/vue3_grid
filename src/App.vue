<template lang="pug">
#app
  h1 VueGrid
  .container
    .row(v-for="row in grid")
      .cell(v-for="col in row")
        span
  .grid__control
    h2 Grid Size
    input#cols(type="range", min="1", max="10", v-model="cols")
    input#rows(type="range", min="1", max="10", v-model="rows")
</template>

<script setup>
import { ref } from "vue";

import { makeGrid } from "./grid";

const cols = ref(2);
const rows = ref(2);
const grid = makeGrid(cols, rows);
</script>

<style lang="stylus">
body, h1, h2 {
  margin: 0;
}

* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e9c46a;
  height: 100vh;
  background-color: #264653;
}

.container {
  background-color: #023047;
  margin-top: 2rem;
  padding: 2rem;
}

.row {
  // background-color #666
  margin: 12px auto;
  width: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.cell {
  border: 1px solid #2a9d8f;
  margin: 12px;
  min-height: 2rem;
  min-width: 2rem;
  cursor: pointer;

  &:hover {
    background-color: #457b9d;
    border: none;
  }
}

.grid__control {
  background-color: #000814;
}
</style>
