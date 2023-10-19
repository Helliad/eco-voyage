<template>
  <NavBar/>
  <LandingPage />
  <ChatBot/>
  <QuickLinks/>
  <FooterBar/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import LandingPage from './components/LandingPage.vue'
import NavBar from './components/NavBar.vue'
import ChatBot from './components/ChatBot.vue'
import QuickLinks from './components/QuickLinks.vue'
import FooterBar from './components/FooterBar.vue'

export default {
  name: 'App',
  components: {
    LandingPage,NavBar,ChatBot,FooterBar,QuickLinks
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
