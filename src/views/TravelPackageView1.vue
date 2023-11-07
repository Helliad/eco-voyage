<template>
    <NavBar/>
    <div class="container">
      <div class="row">
        <div class="col-8">
          <TravelPackage1/>
        </div>
        <div class="col">
          test
        </div>
      </div>
    </div>
    <FooterBar/>
  </template>
  
  <script>
  import NavBar from '@/components/NavBar.vue'
  import FooterBar from '@/components/FooterBar.vue'
  import TravelPackage1 from '@/components/TravelPackage1.vue'
  
  export default {
    name: 'CalculatorView',
    components: {
      NavBar,FooterBar,TravelPackage1
    }
  }
  </script>
  