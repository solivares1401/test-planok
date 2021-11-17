<template>
  <div id="app"> 
  <div class="container">
    <Listado/>
    <Paginador/>
  </div>    
    
  </div>
</template>

<script>
import Listado from './components/Listado.vue'
import Paginador from './components/Paginador.vue'

export default {
  name: 'App',
  components: {    
    Listado,
    Paginador
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
  margin-top: 60px;
}
</style>
