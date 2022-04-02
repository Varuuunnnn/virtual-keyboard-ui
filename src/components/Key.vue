<template>
  <button
    @click="onClickButton"
    class="text-black cursor-pointer rounded-borders"
  >
    {{ name }}
  </button>
</template>

<script>
export default {
  name: "Key",
  props: ["name", "type"],
  methods: {
    onClickButton() {
      this.$emit("clicked", [this.type, this.name]);
    }
  }
};
</script>

<style scoped>
button {
  transition-duration: 0.2s;
  border: 1px solid white;
  background: white;
  min-width: 30px;
  margin: 2px;
}
button:hover {
  border: 1px solid black;
}
</style>
