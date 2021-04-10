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
        this.$emit('show-DetailsCard', this.pokeNumber)
      }
  }
};
</script>

<style scoped>
#poke-card{
    margin-bottom: 25px;
    width: 250px;
    box-shadow: 0 10px 20px 0 rgba(5, 5, 5, 0.863), 0 10px 10px 0 rgba(125, 128, 127, 0.897);
}
.card-btn{
    background-color: #f9f6d8;
    height: 170px;
}
.title{
    width: fit-content
}
p{
    background-color:#454544;
    color: #f5e201;
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
