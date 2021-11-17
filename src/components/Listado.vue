<template>  
    <div class="row">
          <div class="col-md-3" v-for="(item, index) in personajes">                                 
                <div class="card" style="width: 18rem;">
                  <img :src=item.image class="card-img-top" alt="{{item.name}}">
                  <br/>
                  <h5 class="card-title">{{item.name}}</h5>
                    <div class="card-body">
                      <ul class="list-group list-group-flush">
                        <li class="list-group-item">Gender: {{item.gender}}</li>
                        <li class="list-group-item">Status: {{item.status}}</li>
                        <li class="list-group-item">Species: {{item.species}}</li>
                      </ul>
                    </div>
                </div> 
                <br/><br/>                     
          </div>  
      </div>  
    <button type="button" class="btn btn-primary">Primary</button>           
</template>

<script>

export default {
  name: 'Listado',
  props: {
    msg: String
  },
  data: function(){
    return{
        personajes:{}
    }
  },
  mounted: function() {
      console.log("componente montado!", this.loadData());
      
  },
  methods:{
    async loadData(){
      try{
       const res = await fetch("https://rickandmortyapi.com/api/character");
       const data = await res.json();       
       this.personajes = data.results;
      }catch(e){
        console.log("Error", e);
      }
    }
  }
}
</script>

<style scoped>

</style>
