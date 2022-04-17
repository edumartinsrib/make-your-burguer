<template>
  <navBar :logo="logo_src" :alt="app_name" />
  <router-view class="mb-20 tamanho" />
  <footerBar />
</template>
<script>
import navBar from './components/navBar.vue'
import footerBar from './components/footerBar.vue'

export default {
    name: 'App',
    components:{
      navBar, 
      footerBar
    },
    data(){
      return{
        logo_src: '/img/logo.png',
        app_name: 'make your burguer'
      }
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

nav {
  padding: 30px;
}
.tamanho{
  padding-block-end: 100px;
}

nav a {
  font-weight: bold;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
