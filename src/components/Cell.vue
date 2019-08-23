<template>
  <div class="cell" @click="handleCellClick">
    <template v-if="flag">{{content}}</template>
    <template v-else></template>
  </div>
</template>
<script>
export default {
  props: ["step"],
  data() {
    return {
      flag: false,
      content: "",
    }
  },
  methods: {
    handleCellClick() {
      if (this.content) return
      this.flag = true
      this.content = this.step % 2 === 0 ? "X" : "O"
      this.$emit("click", this.content)
    },
  },
}
</script>
<style>
.cell {
  border: 1px solid black;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 80px;
}
</style>