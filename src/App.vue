<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row>
        <b-col>
          <b-card-group deck>
            <h2 id="main-title">Pega os Pokemon</h2>
            <div v-for="(pokemon, index) in pokemonList" :key="index">
              <Pokemon
                :pokeNumber="index + 1"
                :name="pokemon.name"
                :url="pokemon.url"
                v-on:show-DetailsCard="showDetailsCard"
                :pokeColor='pokeColor'
              />
            </div>
          </b-card-group>
        </b-col>

        <b-col no-body class="rounded-0">
          <PokeBigCard v-if="showCard" />
          <PokeDetails
              v-if="!showCard"
              :url="pokeLink"
              :pokeNumber="pokemonNumber"/>
              
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
import PokeBigCard from "./components/PokeBigCard";
import PokeDetails from "./components/PokeDetails";

export default {
  name: "App",
  data() {
    return {
      pokemonList: [],
      showCard: true,
      pokemonUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokeColor:'black',
      pokemonNumber: 0,
      pokeLink: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=10&offset=0")
      .then((res) => {
        console.log(res.data.results);
        this.pokemonList = res.data.results;
      })
      .catch((err) => console.log(err));
  },
  components: {
    Pokemon,
    PokeBigCard,
    PokeDetails,
  },
  methods: {
    showDetailsCard: function (pokeNumber) {
      this.showCard = !this.showCard;
      this.pokemonNumber = pokeNumber;
      this.pokeLink = this.pokemonUrl + this.pokemonNumber;
    },
  },
};
</script>

<style>
#app {
  align-items: center;
  justify-content: space-between;
}
#main-title {
  color: #454545;
  margin: 30px;
}
.rounded-0{
  flex-wrap: wrap;
  display: flex;
}
</style>
