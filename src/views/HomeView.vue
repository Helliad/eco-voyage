<template>
  <NavBar/>
  <LandingPage />
  <ChatBot/>
  <QuickLinks/>
  <TravelReview/>
  <FooterBar/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import LandingPage from '@/components/LandingPage.vue'
import NavBar from '@/components/NavBar.vue'
import ChatBot from '@/components/ChatBot.vue'
import QuickLinks from '@/components/QuickLinks.vue'
import TravelReview from '@/components/TravelReview.vue'
import FooterBar from '@/components/FooterBar.vue'

// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    LandingPage,NavBar,ChatBot,FooterBar,QuickLinks,TravelReview
  }
}
</script>
