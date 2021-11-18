<template>
  <nav aria-label="Page navigation example" v-if="!loading">
    <ul class="pagination"> 
    <!--boton icono << --> 
      <li class="page-item" :class="[page <= 1 ? 'disabled' : '']">
          <a class="page-link" href="javascript:void(0)" tabindex="-1" :aria-disabled="true" @click="page = 1">
          <i class="bi bi-arrow-left"></i>
          </a>
      </li> 
      <!--boton previo -->    
       <li class="page-item" :class="[page <= 1 ? 'disabled' : '']">
          <a class="page-link" href="javascript:void(0)" tabindex="-1" :aria-disabled="true" @click="page--">
            Previous
          </a>
      </li>
      <!--listado de numeros -->
      <li class="page-item" v-for="pageNumber in pages.slice(page-1,page+9)" @click="page = pageNumber" :class="[pageNumber == page ? 'active':'']" v-bind:key=pageNumber>
        <a class="page-link" v-if="pageNumber != pages.length">{{ pageNumber}}</a>
      </li>
      <li v-if="page < pages.length && pages.length > 10" class="page-item">
          <a class="page-link">
              ...
          </a>
      </li>
      <!--boton página final --> 
      <li class="page-item" :class="[page >= totPages ? 'active' : '']">
          <a class="page-link" href="javascript:void(0)" @click="page = pages.length">
              {{pages.length}}
          </a>
      </li>
      <!--boton next --> 
      <li class="page-item" :class="[page >= totPages ? 'disabled' : '']">
            <a class="page-link" href="javascript:void(0)" @click="page++">
                Next
            </a>
        </li> 
            <!--boton icono << --> 
      <li class="page-item" :class="[page == totPages ? 'disabled' : '']">
          <a class="page-link" href="javascript:void(0)" tabindex="-1" :aria-disabled="true" @click="page = totPages">
          <i class="bi bi-arrow-right"></i>
          </a>
      </li>      
    </ul>
  </nav> 
</template>

<script>

export default {
  name: 'Paginador',
  props: {
    pages:Array,
    totPages: Number,
    accion:Function,
    paginaActual:Number
  },
  data(){
    return{
      loading:true,
      perPage: 20,
      page:this.paginaActual,               
    }
  },
  async mounted() { 
    //Se transforma en array el total de páginas          
    this.loading=false;    
  },
  watch:{
    page(){  
      //Se llama la función del componente padre           
      this.$emit('accion', this.page)       
    }
  }
}
</script>

<style scoped>

</style>
