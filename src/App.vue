<template>
  <header>
    <h2>BitPanda Currency Converter</h2>
  </header>
  <div class="container">
    <input-field></input-field>
  </div>
</template>

<script>
import InputField from "./components/InputField.vue";

export default {
  name: "App",
  components: {
    InputField,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  background-color: #ccc;
  border-radius: 7px;
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
  justify-content: space-around;
}
</style>
