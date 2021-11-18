<template>
<form class="row g-3">
    <div class="col-auto">
        <!--Select para ordenar por Nombre y Genero -->
        <select v-if="!loading" class="form-select orderby" aria-label="Default select" v-model="order" @change="sortBy(order)">
            <option selected>Ordenar por:</option>
            <option v-for="(item) in opciones" :value=item v-bind:key=item>{{item}}</option>
        </select>
    </div>
    <div class="col-auto">
        <div v-if="descendente">
            <i class="bi bi-arrow-down iconButton" @click="descendente = false"></i>
        </div>
        <div v-if="!descendente">
            <i class="bi bi-arrow-up iconButton" @click="descendente = true"></i>
        </div>
    </div>
</form>
<br />
</template>

<script>
export default {
    name: 'OrderBy',
    props: {
        accion: Function
    },
    data() {
        return {
            loading: true,
            descendente: true,
            opciones: ['Nombre', 'Género'],
            order:'Ordenar por:'
        }
    },
    mounted() {
        this.loading = false;
        console.log("orderby montado", this.opciones);
    },

    methods:{
        sortBy(e){   
            console.log("orderBy",e);                                           
            this.$emit('accion', {sort:e, desc:this.descendente}) 
        }        
    },
    watch:{
        descendente(){
            this.$emit('accion', {sort:this.order, desc:this.descendente})
        }

    }
}
</script>

<style scoped>
.sortBy {
    width: 150px;
}
.iconButton{
    cursor: pointer;
}
</style>
