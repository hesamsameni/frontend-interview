<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <Header />
        <Resume />
        <Game />
        <Footer />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/layouts/Header.vue";
import Footer from "./components/layouts/Footer.vue";
import Game from "./components/game.vue";
import Resume from "./components/resume.vue";
export default {
  name: "App",
  components: {
    Header,
    Game,
    Resume,
    Footer,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
