<template>
  <div id="app">
    <TimerComponent />
  </div>
</template>

  <script>
import TimerComponent from "./components/timer-component.vue";

export default {
  name: "App",
  components: {
    TimerComponent,
  },
};
</script>

<style>
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

body {
  font-family: sans-serif;
  padding: 0;
  margin: 0;
}

#app {
  height: 100vh;
  text-align: center;
  padding: 10px;
  margin: 0 auto;
  overflow: hidden;
}
</style>
