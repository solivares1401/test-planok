<template>
<form class="row g-3">
    <div class="col-auto">
        <!--Select para ordenar por Nombre y Genero -->
        <select v-if="!loading" class="form-select orderby" aria-label="Default select" v-model="orderBy">
            <option selected>Ordenar por</option>
            <option v-for="(item, index) in opciones" :value=item>{{item}}</option>
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
        }
    },
    mounted() {
        this.loading = false;
        console.log("orderby montado", this.opciones);
    },
    orderBy() {

    }
}
</script>

<style scoped>
.orderby {
    width: 150px;
}
.iconButton{
    cursor: pointer;
}
</style>
