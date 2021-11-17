<template>  
    <div class="row" v-if="!loading">
          <div class="col-md-2"></div>
          <div class="col-md-8">   
            <Paginador :pagesProps=pages @accion=loadData />
              <div class="list-group listado" v-for="(item, index) in personajes">
              <button type="button" class="list-group-item list-group-item-action">
                <b>{{item.id}}</b>. {{item.name}} 
                <img :src=item.image class="rounded-circle thumb float-end" />
              </button>    
              </div>                                           
          </div>  
          <div class="col-md-2"></div>          
    </div>  
    <br/><br/>             
</template>

<script>
import Paginador from './Paginador.vue'

export default {
  name: 'Listado',    
  components:{
    Paginador
  },
  data(){
    return{
        loading:true,
        personajes:{},
        pages:null,
        currentPage:1,
        next:null,
        prev:null
    }
  },
  async mounted() {
      console.log("componente montado!");  
      await this.loadData()    
  },
  methods:{
    async loadData(n){
      console.log("n", n);
      try{
       const res = await fetch(`https://rickandmortyapi.com/api/character/?page=${n ? n : 1}`);
       const data = await res.json();       
       this.personajes = data.results;
       this.loading = false;
       this.pages = data.info.pages;
       this.next = data.info.next;
       this.prev = data.info.prev;
      }catch(e){
        console.log("Error", e);
      }
    },    
  }
}
</script>

<style scoped>
.listado{
  width:100%;
  text-align:left;
}
.thumb{
  width:30px;
}
</style>
