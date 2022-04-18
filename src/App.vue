<template>
  <Navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer/>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default {
  components:{
    Navbar,
    Footer
  },
  data(){
    return{
      logo_src: '/img/logo navbar.png',
      app_name: 'Make Burger'
    }
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
    font-family: helvetica;
    margin: 0;
    padding: 0;
    text-decoration: none;
    list-style: none;
  }

  .main-container{
    margin: 50px;
    min-height: 250px;
  }

  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #ba322b;
  }
</style>
