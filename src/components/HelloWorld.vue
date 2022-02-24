<template>
  <div>
    <h1 class="titulo">PokeGuia</h1>
    <label for="">Pokemon:</label>
    <input type="text" v-model="pokemon.name">
    <button @click="getPokemon" class="button">Buscar</button>
    <div class="row d-flex justify-content-center flex-nowrap">
    <div class="col-md-6">
      <img :src="getImage" class="imagepokemon" alt="...">
      <div class="card-body">
        <h2 class="">{{pokemon.name}}</h2>
      </div>
    </div>
    </div>
    <h3>Movimientos</h3>
    <div  v-for = "(getMove, index) in  getMoves" :key="index">
      
      <p>{{getMove.move.name}}</p>
  
    </div>
    <h3>Habilidades</h3>
    <div  v-for = "(getAbility, index) in  getAbilities" :key="index">
      
      <p>{{getAbility.ability.name}}</p>
  
    </div>
    
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line
  name: "Pokeapp", 
  data(){
    return{
      pokemon: {
      name: "mewtwo",
      sprites:{
        front_default: "",
      },
      abilities: [],
      moves: [],
    },
    };
   
  },
 
  created() {
    this.getPokemon();
  },
  methods: {
    getPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`)
        .then((response) => response.json())
        .then((json) => (this.pokemon = json));
    },
  },
  computed: {
    getImage() {
      return this.pokemon.sprites.other.dream_world.front_default;
    },
    getMoves() {
      return this.pokemon.moves;
    },
    getAbilities() {
      return this.pokemon.abilities;
    },
    getName() {
      return this.pokemon.name;
    },
  },
};
</script>

<style>
.titulo {
  font-size: xx-large;
  margin-bottom: 3%;
}

h2 {
  font-size: x-large;
}

.imagepokemon {
  margin-top: 3%;
}

.button {
  margin-left: 1%;
}
</style>