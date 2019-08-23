<template>
  <div id="app">
    <div>当前步数为{{step}}</div>
    <div class="row">
      <Cell @click="onCellClick(0, $event)" :step="step" />
      <Cell @click="onCellClick(1, $event)" :step="step" />
      <Cell @click="onCellClick(2, $event)" :step="step" />
    </div>
    <div class="row">
      <Cell @click="onCellClick(3, $event)" :step="step" />
      <Cell @click="onCellClick(4, $event)" :step="step" />
      <Cell @click="onCellClick(5, $event)" :step="step" />
    </div>
    <div class="row">
      <Cell @click="onCellClick(6, $event)" :step="step" />
      <Cell @click="onCellClick(7, $event)" :step="step" />
      <Cell @click="onCellClick(8, $event)" :step="step" />
    </div>
    <div>结果：{{result === '' ? '胜负未分': `胜方为${result}`}}</div>
  </div>
</template>

<script>
import Cell from "./components/Cell"
export default {
  data() {
    return {
      step: 0,
      map: [[null, null, null], [null, null, null], [null, null, null]],
      result: "",
    }
  },
  components: {
    Cell,
  },
  methods: {
    onCellClick(index, content) {
      this.map[Math.floor(index / 3)][index % 3] = content
      this.step++
      this.tell()
    },
    tell() {
      const map = this.map
      for (let row = 0; row < 2; row++) {
        if (
          map[row][0] === map[row][1] &&
          map[row][1] === map[row][2] &&
          map[row][2] !== null
        ) {
          this.result = map[row][2]
        }
      }
      for (let col = 0; col < 2; col++) {
        if (
          map[0][col] === map[1][col] &&
          map[1][col] === map[2][col] &&
          map[2][col] !== null
        ) {
          this.result = map[2][col]
        }
      }
      if (
        map[0][0] === map[1][1] &&
        map[1][1] === map[2][2] &&
        map[2][2] !== null
      ) {
        this.result = map[2][2]
      }
      if (
        map[2][0] === map[1][1] &&
        map[1][1] === map[0][2] &&
        map[0][2] !== null
      ) {
        this.result = map[0][2]
      }
    },
  },
}
</script>

<style>
#app {
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  align-items: center;
}

.row {
  display: flex;
  flex-flow: row nowrap;
}
</style>
