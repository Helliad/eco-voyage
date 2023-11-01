<template>
  <NavBar/>
  <LandingPage />
  <QuickLinks/>
  <TravelReview/>
  <FooterBar/>
</template>

<script>
import LandingPage from '@/components/LandingPage.vue'
import NavBar from '@/components/NavBar.vue'
import QuickLinks from '@/components/QuickLinks.vue'
import TravelReview from '@/components/TravelReview.vue'
import FooterBar from '@/components/FooterBar.vue'

export default {
  name: 'HomeView',
  components: {
    LandingPage, NavBar, FooterBar, QuickLinks, TravelReview
}
}
</script>
