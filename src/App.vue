<template>
  <Navbar :logo="src_logo" :alt="App_name"/>
  <router-view/>
  <FooterVue/>
</template>


<script>
import FooterVue from './components/Footer.vue';
import Navbar from './components/Navbar.vue';
export default {
  name: 'App',
  components: {
    Navbar,
    FooterVue
  },
  data(){
    return {
      src_logo: '/img/logo.png',
      App_name: 'Make Your Burger'
    }
  }
}
</script>


<style>
  *{
    font-family: Helvetica, Arial, sans-serif;
    padding: 0;
    margin:0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
