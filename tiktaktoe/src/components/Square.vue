<template>
  <button
    class="square"
    :class="[value, { winner: winner }]"
    :disabled="disabled"
    @click="click"
  >
    {{ value }}
  </button>
</template>

<script>
export default {
  name: "Square",
  props: {
    value: String,
    winner: Boolean,
    disabled: Boolean,
  },
  methods: {
    click() {
      this.$emit("click");
    },
  },
};
</script>

<style scoped>
.square {
  background: #fff9;
  background-blend-mode: exclusion;
  border: 1px solid #ededed;
  font-size: 15vmin;
  font-weight: bold;
  line-height: 34px;
  padding: 0;
  text-align: center;
  transition: all 0.25s ease;
  outline: none;
  text-shadow: -1px -1px 1px #FF5C5B, -1px 1px 1px #FF5C5B, 1px -1px 1px #FF5C5B, 1px 1px 1px #FF5C5B;
}
.square.winner {
  background: #50CB93;
}
.square:not([disabled]):empty:hover,
.square:not([disabled]):empty:focus {
  box-shadow: inset 0 2px 25px #ededed;
  cursor: pointer;
}
.square:not([disabled]):empty:active {
  box-shadow: inset 0 2px 50px #ededed;
}
.square.X {
  color: #FF5C5B;
}
.square.O {
  color: white;
}
</style>
