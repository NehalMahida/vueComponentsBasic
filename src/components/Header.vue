<template>
  <header>
    <h2 @click="backToHome()">BigBucket</h2>
  </header>
</template>

<script>
export default {
  methods: {
    // when click on a title go back to home page.
    backToHome() {
      this.emitter.emit("backToHome", "Products");
    },
  },
};
</script>

<style scoped>
header {
  width: 100%;
  height: 50x;
  background: #333;
  color: #eee;
}
h2 {
  padding: 10px;
  cursor: pointer;
}
</style>
