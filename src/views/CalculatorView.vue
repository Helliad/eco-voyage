<template>
  <NavBar/>
  <CalculatorEmissions/>
  <FooterBar/>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import FooterBar from '@/components/FooterBar.vue'
import CalculatorEmissions from '@/components/CalculatorEmissions.vue'

export default {
  name: 'CalculatorView',
  components: {
    NavBar,CalculatorEmissions,FooterBar
  }
}
</script>
