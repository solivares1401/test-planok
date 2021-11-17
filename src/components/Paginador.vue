<template>
  <nav aria-label="Page navigation example" v-if="!loading">
    <ul class="pagination"> 
      <li class="page-item" :class="[page <= 1 ? 'disabled' : '']">
          <a class="page-link" href="javascript:void(0)" tabindex="-1" :aria-disabled="true" @click="page = 1">
          <span aria-hidden="true">&laquo;</span>
          </a>
      </li>     
       <li class="page-item" :class="[page <= 1 ? 'disabled' : '']">
          <a class="page-link" href="javascript:void(0)" tabindex="-1" :aria-disabled="true" @click="page--">
            Previous
          </a>
      </li>
      <li class="page-item" v-for="pageNumber in pages.slice(page-1,page+9)" @click="page = pageNumber" :class="[pageNumber == page ? 'active':'']">
        <a class="page-link" v-if="pageNumber != pages.length">{{ pageNumber}}</a>
      </li>
      <li v-if="page < pages.length && pages.length > 10" class="page-item">
          <a class="page-link">
              ...
          </a>
      </li>
      <li class="page-item" :class="[page >= totPages ? 'active' : '']">
          <a class="page-link" href="javascript:void(0)" @click="page = pages.length">
              {{pages.length}}
          </a>
      </li>
      <li class="page-item" :class="[page >= totPages ? 'disabled' : '']">
            <a class="page-link" href="javascript:void(0)" @click="page++">
                Next
            </a>
        </li>      
    </ul>
  </nav> 
</template>

<script>

export default {
  name: 'Paginador',
  props: {
    pagesProps:Number,
    accion:Function,
    paginaActual:Number
  },
  data(){
    return{
      loading:true,
      perPage: 20,
      page:this.paginaActual,
      totPages: this.pagesProps,    
      pages:0 
    }
  },
  async mounted() {      
    this.pages = Array.from({length: this.pagesProps}, (v, i) => i+1)  
    this.loading=false;
  },
  watch:{
    page(){             
      this.$emit('accion', this.page)       
    }
  }
}
</script>

<style scoped>

</style>
