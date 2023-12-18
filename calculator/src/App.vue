<template>
  <div>
    <h1>Calculadora</h1>
    <MainCalculadora />
  </div>
</template>

<script>
import MainCalculadora from "./components/MainCalculadora";

export default {
  name: "App",
  components: { MainCalculadora },
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;

  color: white;
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(1, 112, 152, 1) 53%,
    rgba(1, 135, 176, 1) 64%,
    rgba(0, 212, 255, 1) 100%
  );
}
</style>
