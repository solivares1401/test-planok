<template>
<div v-if="!loading">
    <div class="card cartilla" style="width: 18rem;">
        <img :src=personaje.image class="card-img-top" :alt=personaje.name>
        <div class="card-body">
            <h5 class="card-title"><b>{{personaje.name}}</b></h5>           
            <p class="card-text">Status: {{personaje.status}}<br/>
            Species:{{ personaje.species}}<br/>
            Gender: {{personaje.gender}}<br/>            
            </p>        
            <a href="#" class="btn btn-light" @click="this.$emit('accion')"><i class="bi bi-arrow-left"></i> Volver</a>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'Detalle',
    props: {
        id: Number,
        accion:Function        
    },
    data() {
        return {
            personaje: null,
            loading: true
        }
    },
    async mounted() {
        console.log("detalle montado", this.id);
        await this.loadData();
    },
    methods: {
        async loadData() {
            try {
                const res = await fetch(`https://rickandmortyapi.com/api/character/${this.id}`);
                const data = await res.json();                
                this.personaje = data;
                this.loading = false;
            } catch (error) {
                console.log("error", error);
            }
        }
    }
}
</script>

<style scoped>
.cartilla{
 margin: 0 auto;
}
</style>
