<template>
  <div class="board" v-if="squares">
    <div v-for="row in 3" :key="row" class="board-row">
      <square
        v-for="i in 3"
        :key="indexByRow(i, row)"
        :value="squares[indexByRow(i, row)]"
        :disabled="!!winner"
        :winner="!!winner && winner.includes(indexByRow(i, row))"
        @click="click(i, row)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",
  props: {
    squares: Array,
    winner: Array,
  },
  components: {
    Square: () => import("./Square"),
  },
  methods: {
    indexByRow(index, row, max = 3) {
      return row * max + index - (max + 1);
    },
    click(index, row) {
      this.$emit("click", this.indexByRow(index, row));
    },
  },
};
</script>

<style scoped lang="scss">
.board {
  box-shadow: 2.5px 5px 25px #ededed, 0 1px 6px #ededed;
  border-radius: 0.5rem;
  width: 65vmin;
  height: 65vmin;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, 1fr);
  @media (max-width: 768px) {
    margin-bottom: 30px;
  }
}
.board-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
}
</style>
