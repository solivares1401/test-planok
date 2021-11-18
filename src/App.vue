<template>
<div id="app">
    <div class="container">
        <h2>Test para PlanOk </h2>
        <p>Desarrollado por Sebastián Olivares</p>
        <br/>
        <Listado />
    </div>
</div>
</template>

<script>
import Listado from './components/Listado.vue'

export default {
    name: 'App',
    components: {
        Listado,
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
