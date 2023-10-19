<template>
  <NavBar/>
  <CalculatorEmissions/>
  <!-- <ChatBot/> -->
  <FooterBar/>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
// import ChatBot from '@/components/ChatBot.vue'
import FooterBar from '@/components/FooterBar.vue'
import CalculatorEmissions from '@/components/CalculatorEmissions.vue'

export default {
  name: 'CalculatorView',
  components: {
    NavBar,CalculatorEmissions,
    // ChatBot,
    FooterBar
  }
}
</script>
