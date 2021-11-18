<template>
<!--Buscador con filtros -->
<!--La api no tiene información con respecto a Edad para utilizar en los filtros -->

<form class="row g-3">
    <div class="col-auto">
        <label for="buscar" class="visually-hidden">Buscar:</label>
        <input type="text" class="form-control" id="buscar" placeholder="Buscar..." v-model="txtBuscar">
    </div>
    <div class="col-auto">
        <select class="form-select orderby" aria-label="Default select" v-model="filterSelected">
            <option v-for="(item) in filtros" :value=item v-bind:key=item>{{item}}</option>
        </select>
    </div>
    <div class="col-auto">
        <button type="submit" class="btn btn-primary mb-3" @click="search">Buscar</button>
    </div>    
</form>

<br />
</template>

<script>

export default {
    name: 'Buscador',
    props: {        
        accion:Function        
    },
    data() {
        return {
            loading: true,
            filtros: ['Nombre', 'Género'],
            txtBuscar:'',
            filterSelected:'Nombre'            
        }
    },
    mounted() {
        this.loading = false;        
    },
    methods:{
        search(){                                              
            this.$emit('accion', {filter:this.filterSelected, txt:this.txtBuscar}) 
        }        
    }
}
</script>

<style scoped>
.orderby {
    width: 150px;
}
</style>
