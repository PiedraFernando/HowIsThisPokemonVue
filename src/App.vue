<template>
  <h1 class="text-center mt-3">who Is this Pokemon</h1>
  <p class="text-center">Game about, guess what pokemon it is. By: Fernando Piedra Mendez &lt;OnlyKal&gt;</p>
  <div class="d-flex justify-content-evenly">
    <div class="w-25">
      <NumberComponent @changeNumber="setGeneration($event)" maxNumber="7" title="Generation"/>
    </div>
    <div class="w-25">
      <NumberComponent @changeNumber="setDifficulty($event)" maxNumber="2" title="Difficulty"/>
    </div>
  </div>
  <div class="d-flex justify-content-center mt-3">
    <h3 class="m-3">hits: {{corrects}}</h3>
    <h3 class="m-3">mistakes: {{errors}}</h3>
  </div>
  <div>
    <div class="d-flex justify-content-center mt-1">
      <Pokemon :nombre="nameAnsware" :img="img" :status="status"/>
    </div>
  </div>
  <h2 class="text-center mt-3">who is?</h2>
  <OptionsComponent :name1="name1" :name2="name2" :name3="name3" @check="check($event)"/>
</template>

<script>
import Pokemon from "./components/Pokemon.vue";
import NumberComponent from "./components/NumberComponent.vue"
import OptionsComponent from "./components/OptionsComponent.vue"

export default {
  name: 'App',
  components: {
    Pokemon,
    NumberComponent,
    OptionsComponent
  },
  data(){
    return{
      maxPokemon:151,
      difficulty:1,
      nameAnsware: null,
      errors:0,
      corrects:0,
      status: 'ask',
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
      this.status = 'ask'
      fetch('https://pokeapi.co/api/v2/pokemon/' + (Math.floor(Math.random() * this.maxPokemon) + 1))
        .then(response => response.json())
        .then(data => {
          let num = Math.floor(Math.random() * 3) + 1
          if(this.difficulty === 1){
            this.img = data.sprites.front_default
          }else{
            this.img = data.sprites.back_default
            if(!this.img){
              this.img = data.sprites.front_default
            }
          }
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
    check(val){
      if(this.nameAnsware === val){
        this.corrects ++;
        this.status = 'correct'
      }else{
        this.errors ++;
        this.status = 'mistake'
      }
      this.restartName()
    },
    restartName(){
      setTimeout(() => {
        this.name1 = null
        this.name2 = null
        this.name3 = null
        this.status = false
        this.getAskPokemon()
      }, 1100);
    },
    setGeneration(val){
      switch (val) {
        case 1:
            this.maxPokemon=151
          break;
        case 2:
            this.maxPokemon=251
          break;
        case 3:
            this.maxPokemon=386
          break;
        case 4:
            this.maxPokemon=493
          break;
        case 5:
            this.maxPokemon=649
          break;
        case 6:
            this.maxPokemon=721
          break;
        case 7:
            this.maxPokemon=809
          break;
        default:
            this.maxPokemon=151
          break;
      }
    },
    setDifficulty(val){
      this.difficulty = val
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
