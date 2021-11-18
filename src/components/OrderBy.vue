
<template>
<!--Select para ordenar por Nombre y Genero --> 
<select v-if="!loading" class="form-select orderby" aria-label="Default select">
  <option selected>Ordenar por</option>
  <option v-for="(item, index) in opciones" :value=item>{{item}}</option>  
</select>
<br/>
</template>
<script>
export default {
    name: 'OrderBy',
    data(){
        return {
            loading:true,
            opciones:['Nombre','Género'],
        }
    },
    mounted() {
        this.loading=false;        
        console.log("orderby montado", this.opciones);
    }
}
</script>

<style scoped>
    .orderby{
        width:150px;
    }
</style>