<template>
  <NavBar/>
  <LandingPage />
  <ChatBot/>
  <FooterBar/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import LandingPage from './components/LandingPage.vue'
import NavBar from './components/NavBar.vue'
import ChatBot from './components/ChatBot.vue'
import FooterBar from './components/FooterBar.vue'

export default {
  name: 'App',
  components: {
    LandingPage,NavBar,ChatBot,FooterBar
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
