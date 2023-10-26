<template>
  <NavBar/>
  <VehicleRental/>
  <CarCalculatorEmissions/>
  <FooterBar/>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import FooterBar from '@/components/FooterBar.vue'
import VehicleRental from '@/components/VehicleRental.vue'
import CarCalculatorEmissions from '@/components/CarCalculatorEmissions.vue'

export default {
  name: 'RentalView',
  components: {
    NavBar,VehicleRental,FooterBar,CarCalculatorEmissions
  }
}
</script>
