<template>
    <button @click="toggleTheme">Zmień motyw</button>
  </template>
  
  <script>
  export default {
    name: "ThemeButton",
    methods: {
      toggleTheme() {
        this.$emit("toggle-theme"); 
      },
    },
  };
  </script>
  
 