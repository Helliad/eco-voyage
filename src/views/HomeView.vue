<template>
  <NavBar/>
  <LandingPage />
  <QuickLinks/>
  <TravelPackages/>
  <FooterBar/>
</template>

<script>
import LandingPage from '@/components/LandingPage.vue'
import NavBar from '@/components/NavBar.vue'
import QuickLinks from '@/components/QuickLinks.vue'
import FooterBar from '@/components/FooterBar.vue'
import TravelPackages from '@/components/TravelPackages.vue'

export default {
  name: 'HomeView',
  components: {
    LandingPage, NavBar, FooterBar, QuickLinks, TravelPackages
}
}
</script>
