<template>
  <Header @openHelp="help = true" />
  <Help @closeHelp="help = false" v-if="help" />
  <Game />
</template>

<script>
import Header from "./components/Header.vue";
import Help from "./components/Help.vue";
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: { Header, Help, Game },
  data() {
    return {
      help: false,
    };
  },
};
</script>

<style>
#app {
  font-family: "Clear Sans", "Helvetica Neue", Arial, sans-serif;
  font-weight: bold;
  letter-spacing: 0.2rem;
  text-transform: uppercase;
  text-align: center;
  color: #d8d8d8;
}

body {
  background-color: rgb(22, 22, 22);
}

.button {
  background-color: #538d4e;
  border: none;
  padding: 15px 32px;
  text-align: center;
  display: inline-block;
  font-size: 16px;
  font-family: "Clear Sans", "Helvetica Neue", Arial, sans-serif;
  font-weight: bold;
  letter-spacing: 0.2rem;
  text-transform: uppercase;
  text-align: center;
  color: #d8d8d8;
  margin: 10px;
  cursor: pointer;
}
</style>
