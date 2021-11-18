<template>
<div v-if="!loading && listView">
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-6">
            <!--buscador -->
            <Buscador @accion=loadDataFiltered />
        </div>
        <div class="col-md-2">
            <!--ordenar por -->
            <OrderBy @accion=loadDataOrderBy />
        </div>
        <div class="col-md-2"></div>
    </div>
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-8">
            <!--Listado de personajes -->
            <div class="list-group listado" v-for="(item) in personajes" v-bind:key=item>
                <button type="button" class="list-group-item list-group-item-action" @click=detalle(item.id)>
                    {{item.name}}
                    <img :src=item.image class="rounded-circle thumb float-end" />
                </button>
            </div>
        </div>
        <div class="col-md-2"></div>
    </div>
    <br/>
     <!--paginador -->
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-8">           
            <Paginador :pages=pages :totPages=totPages @accion=loadData :paginaActual=currentPage />
        </div>
        <div class="col-md-2"></div>
    </div>
</div>

<div v-if="!listView">
    <div class="row">
        <div class="col-md-12">
            <div class="text-center">
                <Detalle :id=idPersonaje @accion=volver />
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Paginador from './Paginador.vue';
import Detalle from './Detalle.vue';
import Buscador from './Buscador.vue';
import OrderBy from './OrderBy.vue';

export default {
    name: 'Listado',
    components: {
        Paginador,
        Detalle,
        Buscador,
        OrderBy
    },
    data() {
        return {
            idPersonaje: null,
            listView: true,
            loading: true,
            personajes: {},
            pages: null,
            totPages: 0,
            next: null,
            prev: null,
            objFilter: {},
            currentPage: null
        }
    },
    async mounted() {
        //Una vez montado el dom inicia la carga de los datos             
        await this.loadData();
    },
    methods: {
        async loadData(n = 1, obj) {
            //guarda en memoria pagina actual
            this.currentPage = n;
            try {
                //Construye url para consulta
                const url = `https://rickandmortyapi.com/api/character/?page=${n}${this.setFiltro(this.objFilter)}`;
                console.log("url", url);
                //Consulta a la api para traer pagina por numero
                const res = await fetch(url);
                const data = await res.json();                
                this.personajes = data.results;
                this.totPages = data.info.pages;
                this.pages = Array.from({
                    length: data.info.pages
                }, (v, i) => i + 1);
                this.next = data.info.next;
                this.prev = data.info.prev;
                this.loading = false;
            } catch (e) {
                console.log("Error", e);
            }
        },
        detalle(id) {
            //Maneja la visualizacion del detalle del personaje pasando el id al componente            
            this.idPersonaje = id;
            this.listView = false;
        },
        volver() {
            //Funcion para cambiar a la vista de listado
            this.listView = true;
        },
        orderBy() {
            console.log();
        },
        async loadDataFiltered(obj) {
            this.objFilter = obj;
            await this.loadData();
        },
        loadDataOrderBy(obj){            
            switch (obj.sort) {
                case 'Nombre':
                    //Ordenar por nombre alfabeticamente
                    if(obj.desc){                        
                        this.personajes.sort((a, b)=> a.name < b.name ? -1 : 1);                                              
                    }else {                        
                      this.personajes.sort((a, b)=> a.name > b.name ? -1 : 1);  
                    }                     
                    break;
                case 'Género':
                    //Ordenar por genero alfabeticamente
                    if(obj.desc){                        
                        this.personajes.sort((a, b)=> a.gender < b.gender ? -1 : 1);
                    }else {                        
                      this.personajes.sort((a, b)=>a.gender > b.gender ? -1 : 1);  
                    }                 
                    break            
                default:
                    break;
            }                      
        },
        setFiltro(obj) {
            let query = '';
            if (obj) {
                switch (obj.filter) {
                    case 'Nombre':
                        query = `&name=${obj.txt}`;
                        break;
                        //La api no trabaja con edad
                    case 'Edad':
                        query = `&name=${obj.txt}`;
                        break;
                    case 'Género':
                        query = `&gender=${obj.txt}`;
                        break;
                    default:
                        break;
                }
            }
            return query;
        }
    }
}
</script>

<style scoped>
.listado {
    width: 100%;
    text-align: left;
}

.thumb {
    width: 30px;
}
</style>
