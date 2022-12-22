<template>
  <div id="app">
    <HeaderComponent/>
    <router-view/>  
    <FooterComponent/>
  </div>
</template>

<script>
import './styles/global.css'
import HeaderComponent from './components/HeaderComponent'
import FooterComponent from './components/FooterComponent';
export default {
  name: 'App',
  components: {
    HeaderComponent, 
    FooterComponent  
  }
}
</script>