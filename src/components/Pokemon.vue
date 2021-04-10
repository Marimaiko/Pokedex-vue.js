<template>
  <div class="cards">
      <b-card no-body class="overflow-hidden" id="poke-card">
        <button class="card-btn" v-on:click="show">
            <b-row no-gutters>
                <b-col md="7">
                    <b-card-body class="title">
                        <h5>#0{{pokeNumber}} <br>{{name | letterUpper}}</h5>
                        <p>{{pokemon.type}} </p>
                        <p v-show='pokemon.type1'>{{pokemon.type1}} </p>
                    </b-card-body>
                </b-col>
                <b-col md="5" >
                    <b-card-img
                        :src='pokemon.img'
                        alt="Image"
                        class="poke-image"
                    ></b-card-img> 
                </b-col>
            </b-row>
        </button>
      </b-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
        this.pokemon.img = res.data.sprites.front_default;
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.type1 = res.data.types[1].type.name;
        console.log(res.data);
    })
    .catch(err => console.log(err));
  },  
  data(){
    return{
        pokemon:{
            img:'',
            type:'',
            type1:'',
            selectedPokemon: ''
        }
      } 
    },
  props: {
    name: String,
    url: String,
    pokeNumber: Number,
  },
 
  filters: {
    letterUpper: function (value) {
      let pokeName = value[0].toUpperCase() + value.slice(1);
      return pokeName;
    },
  },
  methods: {
      show: function(){
        console.log('Filho clicavel')
        this.$emit('show-DetailsCard', this.pokeNumber)
        console.log(this.pokeNumber)
        // this.$emit(this.url)
        // this.$$emit('selectedPokemon', url)
      }
  }
};
</script>

<style scoped>
#poke-card{
    margin-bottom: 25px;
    width: 250px;
    /* min-height: fit-content; */
}
.card-btn{
    background-color: darkgray ;
    height: 170px;
}
.title{
    width: fit-content
}
p{
    background-color:rgba(0, 0, 0, 0.07);
    border-radius: 10px;
    text-align: center;
}
.poke-image{
    image-rendering: -moz-crisp-edges;
    image-rendering: -webkit-crisp-edges;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    min-width: 150px;
    transform:translateX(-30px);
}

</style>
