<template>
  <h1 class="text-center mt-3">How Is this Pokemon</h1>
  <p class="text-center">Game about, how is this pokemon. By: Fernando Piedra Mendez &lt;OnlyKal&gt;</p>
  <div class="d-flex justify-content-center mt-3">
    <h3 class="m-3">Corrects: {{corrects}}</h3>
    <h3 class="m-3">Errors: {{errors}}</h3>
  </div>
  <div class="d-flex justify-content-center mt-5">
    <Pokemon :nombre="nameAnsware" :img="img" :status="status" />
  </div>
  <h2 class="text-center mt-3">How is?</h2>
  <div class="d-flex justify-content-center mt-5">
    <button type="button" class="btn btn-outline-secondary m-2" @click="check1">{{name1}}</button>
    <button type="button" class="btn btn-outline-secondary m-2" @click="check2">{{name2}}</button>
    <button type="button" class="btn btn-outline-secondary m-2" @click="check3">{{name3}}</button>
  </div>
</template>

<script>
import Pokemon from "./components/Pokemon.vue";

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data(){
    return{
      nameAnsware: null,
      errors:0,
      corrects:0,
      status: false,
      name1: null,
      name2: null,
      name3: null,
      img: null
    }
  },
  created(){
    this.getAskPokemon()
  },
  methods:{
    getAskPokemon(){
      fetch('https://pokeapi.co/api/v2/pokemon/' + (Math.floor(Math.random() * 151) + 1))
        .then(response => response.json())
        .then(data => {
          let num = Math.floor(Math.random() * 3) + 1
          this.img = data.sprites.front_default
          this.nameAnsware = data.name
          if(num === 1){
            this.name1 = data.name
          }
          if(num === 2){
            this.name2 = data.name
          }
          if(num === 3){
            this.name3 = data.name
          }
          if(!this.name1){
            fetch('https://pokeapi.co/api/v2/pokemon/' + (Math.floor(Math.random() * 151) + 1))
            .then(response => response.json())
            .then(data => {
              this.name1 = data.name
            })
          }
          if(!this.name2){
            fetch('https://pokeapi.co/api/v2/pokemon/' + (Math.floor(Math.random() * 151) + 1))
            .then(response => response.json())
            .then(data => {
              this.name2 = data.name
            })
          }
          if(!this.name3){
            fetch('https://pokeapi.co/api/v2/pokemon/' + (Math.floor(Math.random() * 151) + 1))
            .then(response => response.json())
            .then(data => {
              this.name3 = data.name
            })
          }
        })
    },
    check1(){
      if(this.nameAnsware === this.name1){
        this.corrects ++;
      }else{
        this.errors ++;
      }
      this.restartName()
    },
    check2(){
      if(this.nameAnsware === this.name2){
        this.corrects ++;
      }else{
        this.errors ++;
      }
      this.restartName()
    },
    check3(){
      if(this.nameAnsware === this.name3){
        this.corrects ++;
      }else{
        this.errors ++;
      }
      this.restartName()
    },
    restartName(){
      this.status = true
      setTimeout(() => {
        this.name1 = null
        this.name2 = null
        this.name3 = null
        this.status = false
        this.getAskPokemon()
      }, 1000);
    }
  }
}
</script>

<style>
*{
    font-family: 'Gochi Hand', cursive;
    font-family: 'Zen Kurenaido', sans-serif;
    background-color: rgb(63, 63, 63);
    color: rgb(221, 221, 221);
}
</style>
