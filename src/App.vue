<template>
  <Section />
</template>

<script>
import Section from "./components/Section.vue";

export default {
  name: "App",
  components: {
    Section,
  },
};
</script>

@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap');

<style>
:root{
  --primary__blue: hsl(238, 40%, 52%);
  --primary__red: hsl(358, 79%, 66%);
  --primary__gray-blue: hsl(239, 57%, 85%);
  --primary__pale-red: hsl(357, 100%, 86%);

  --neutral__blue: hsl(212, 24%, 26%);
  --neutral__gray-blue: hsl(211, 10%, 45%);
  --neutral__light-gray: hsl(223, 19%, 93%);
  --neutral__very-light-gray: hsl(228, 33%, 97%);
  --neutral__white: hsl(0, 0%, 100%);
}

body{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

button { 
  cursor: pointer;
}

#app {
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 20px;
  height: 100vh;
  background: var(--neutral__very-light-gray);
}
</style>
