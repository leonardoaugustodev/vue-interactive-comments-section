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

  --rgb-blue: 84, 87, 182;

  --primary-blue: rgb(var(--rgb-blue));
  --primary-red: rgb(237, 100, 104);
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
  --desktop-borderRadius: 6px;
  --desktop-fontSize: 16px;
  
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

button:hover{
  filter: opacity(0.7);
  transition: all 0.3s ;
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
