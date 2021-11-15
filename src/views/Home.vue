<template>
  <div class="home">
    <br><br><br>
    <HelloWorld msg="Bienvenido"/>

  <div class="row justify-content-center">
    <div class="col-4">
      <img width="300px" alt="Vue logo" src="../assets/search.png">
    </div>
    <div class="col-4">
      <br><br><br><br><br>
      <div class="input-group mb-3">
      <input type="text" class="form-control" placeholder="Digíte una palabra" v-model="word">
      <div class="input-group-append">
        <button class="btn btn-outline-success" v-on:click="searchEngine" >Buscar</button>
      </div>
    </div>

    </div>
  </div>
  <br><br>
   <div class="row justify-content-md-center">
    <div class="col-md-auto">
      
      <div v-for="item in objects" :key="item">
        <h3><span class="badge badge-success">{{item.pageid}} - {{item.title}}</span></h3>
        <p><b>{{item.snippet}}</b></p>
      </div>
      <hr>
    </div>

  </div>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import * as Vue from 'vue' // in Vue 3
import axios from 'axios'
import VueAxios from 'vue-axios'


export default {
  name: 'Home',
  components: {
    HelloWorld
  },

  data(){
    
    return{
      objects : [],
      word : "",
    }

  },

  methods:{
    searchEngine: function(){

      if(this.word.trim() == ""){
        this.$swal('Error','Digíta una palabra!!!');
        this.objects = []
      }else{
          const url = "https://en.wikipedia.org/w/api.php?action=query&list=search&srprop=snippet&format=json&origin=*&utf8=&srsearch="
          axios.get(url+this.word).then(resp => {
          console.log(resp.data.query.search);
          this.objects = resp.data.query.search;
          this.word = ""
      });
      }

    }
  }

}
</script>
