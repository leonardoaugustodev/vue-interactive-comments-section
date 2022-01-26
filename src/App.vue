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
  --primary-blue: hsl(238, 40%, 52%);
  --primary-red: hsl(358, 79%, 66%);
  --primary-grayBlue: hsl(239, 57%, 85%);
  --primary-paleRed: hsl(357, 100%, 86%);

  --neutral-blue: hsl(212, 24%, 26%);
  --neutral-grayBlue: hsl(211, 10%, 45%);
  --neutral-lightGray: hsl(223, 19%, 93%);
  --neutral-veryLightGray: hsl(228, 33%, 97%);
  --neutral-white: hsl(0, 0%, 100%);

  --desktop-maxWidth: 800px;
  --desktop-margin: 20px;
  --desktop-padding: 20px;
  --desktop-borderRadius: 8px;
  --desktop-fontSize: 18px;
  
  --mobile-margin: 10px;
  --mobile-padding: 15px;
  --mobile-borderRadius: 4px;
  --mobile-fontSize: 14px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

button { 
  cursor: pointer;
}
body{
  background: var(--neutral-veryLightGray);
}

#app {
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
  width: 100vw;

  display: flex;
  justify-content: center;
}
</style>
