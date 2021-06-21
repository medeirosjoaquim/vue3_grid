<template lang="pug">
#app
  .title 
    span VueGrid
  //- h1 {{JSON.stringify(grid)}}
  .container
    .row(v-for="row in grid")
      .cell(v-for="col in row" v-on:click="getCell(col)")
        span
  .grid__control
    div
      h2 Grid Size
    .controllers
      div  
        label(for="cols") cols
        input#cols(type="range", 
          min="1", 
          max="8", 
          v-model="cols" 
          v-on:change="updateGrid")
        span {{cols}}
      div
        label(for="cols") rows
        input#rows(type="range", 
          min="1", 
          max="8", 
          v-model="rows" 
          v-on:change="updateGrid")
        span {{rows}}
      
</template>

<script setup>
import { ref, onUpdated, onBeforeUpdate } from "vue"

import { makeGrid } from "./grid"

const cols = ref(2)
const rows = ref(2)
let grid = ref(makeGrid(cols.value, rows.value))
const getCell = (col) => {
  const [x,y] = col
  console.log({x,y})
}
onBeforeUpdate(
  () => {
    grid.value = makeGrid(cols.value, rows.value)
  }
)

</script>

<style lang="stylus">

body, h1, h2 {
  margin: 0
}

* 
  box-sizing: border-box

#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #e9c46a
  height: 100vh
  background-color: #264653
  overflow hidden
  .title
    margin-top 1rem
    text-align: center
    span
      font-size 32px

.container 
  background-color: #023047
  height 36rem
  overflow hidden 

.row 
  // background-color #666
  margin: 12px auto
  width: 200px
  display: flex
  align-items: center
  justify-content: center
  &:not(:last-child)
    .cell
      &:before
        position absolute
        content ""
        top 3rem
        left 1.5rem
        border-left  2px solid white
        height  1.75rem
        // width   2px
        // background-color #666
.cell 
  position relative
  border: 1px solid #2a9d8f
  margin: 8px
  min-height: 3rem
  min-width: 3rem
  border-radius 5px
  cursor: pointer
  &:not(:last-child):after
    position absolute
    content ""
    top 1.4rem
    left 3rem
    border-top  2px solid white
    width 1rem
  
  &:hover 
    background-color: #457b9d

.grid__control 
  display flex
  flex-direction column
  height 8rem
  padding 1.5rem
  background-color: #000814
  .controllers
    display flex

  
</style>
