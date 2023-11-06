<template>
  <div v-html="index"></div>
  </template>
  
  <script>
  import index from "../../pokemon-game/index.html"

  export default {
    data() {
      return {
        isNavbarCollapsed: false,
      };
    },
    methods: {
      toggleNavbarCollapse() {
        this.isNavbarCollapsed = !this.isNavbarCollapsed;
      },
    },
  };
  </script>
  
  <style>
  .navbar-brand {
    font-weight: bold;
    font-size: 1.5rem;
  }
  
  .navbar-nav .nav-link {
    font-size: 1.2rem;
  }
  
  .navbar {
    background-color: rgba(193, 227, 255);
  }
  
  /* 
  .navbar a{
      color: rgb(225, 225, 225);
  } */
  
  .navbar-nav {
    margin-left: auto;
  }
  </style>
  