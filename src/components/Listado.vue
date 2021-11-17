<template>
  <div class="row" v-if="!loading && listView">
      <div class="col-md-2"></div>
      <div class="col-md-8">
          <Paginador :pagesProps=pages @accion=loadData :paginaActual=currentPage />
          <div class="list-group listado" v-for="(item, index) in personajes">
              <button type="button" class="list-group-item list-group-item-action" @click=detalle(item.id)>
                  <b>{{item.id}}</b>. {{item.name}}
                  <img :src=item.image class="rounded-circle thumb float-end" />
              </button>
          </div>
      </div>
      <div class="col-md-2"></div>
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
import Paginador from './Paginador.vue'
import Detalle from './Detalle.vue'

export default {
    name: 'Listado',
    components: {
        Paginador,
        Detalle
    },
    data() {
        return {
            idPersonaje: null,
            listView: true,
            loading: true,
            personajes: {},
            pages: null,
            currentPage: 1,
            next: null,
            prev: null
        }
    },
    async mounted() {   
        //Una vez montado el dom inicia la carga de los datos             
        await this.loadData();
    },
    methods: {
        async loadData(n) {
            //Guarda en memoria la pagina actual
            this.currentPage = n ? n : this.currentPage;
            try {
                //Consulta a la api para traer pagina por numero
                const res = await fetch(`https://rickandmortyapi.com/api/character/?page=${n ? n : this.currentPage}`);
                const data = await res.json();
                this.personajes = data.results;
                this.pages = data.info.pages;
                this.next = data.info.next;
                this.prev = data.info.prev;
                this.loading = false;
            } catch (e) {
                console.log("Error", e);
            }
        },
        detalle(id) {
            console.log("detalle!!!", id);
            this.idPersonaje = id;
            this.listView = false;
        },
        volver(){
          this.listView = true;
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
