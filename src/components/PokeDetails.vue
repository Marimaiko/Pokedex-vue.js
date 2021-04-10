<template>
    <div class="poke-BigCard" >
        <b-card :img-src="pokemon.img" img-alt="Card image" img-top class="photo" ></b-card>
            <b-card-text class="bigCard-title" style="text-align:center">
                <h4>{{pokemon.name | letterUpper}}</h4>
                <p>#0{{pokeNumber}} </p>
            </b-card-text>
            <div class="poke-data">
                <div class="data">
                    <h5>Type:</h5>
                    <p>{{pokemon.type}}</p>
                    <p v-show='pokemon.type1'>{{pokemon.type1}} </p>
                </div>
                <div class="data">
                    <h5>Height:</h5>
                    <p>{{pokemon.height}}m</p>
                </div>
                <div class="data">
                    <h5>Weight:</h5>
                    <p>{{pokemon.weight}}Kg</p>
                </div>
                <div class="data-abi" >
                    <h5>Abilities:</h5>
                    <div class="abili">
                        <p>{{pokemon.abilities}}</p>
                        <p v-show='pokemon.abilities1'>{{pokemon.abilities1}} </p>
                    </div>
                </div>
            </div>
            
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    created: function(){
        axios.get(this.url)
        .then(res => {
            this.pokemon.img = res.data.sprites.front_default;
            this.pokemon.name = res.data.forms[0].name;
            this.pokemon.type = res.data.types[0].type.name;
            if(res.data.types.length>1){
               this.pokemon.type1 = res.data.types[1].type.name;
            }
            this.pokemon.height = res.data.height;
            this.pokemon.weight = res.data.weight;
            this.pokemon.abilities = res.data.abilities[0].ability.name;
            if(res.data.abilities.length>1){
                this.pokemon.abilities1 = res.data.abilities[1].ability.name;
            }
    })
        .catch(err => console.log(err))
},
    data(){
        return{
            pokemon:{
              img:'',  
              name:'',
              type:'',
              type1:'',
              height:'',
              weight:'',
              abilities:'',
              abilities1:''
            }
    }
},
    props:{
        name: String,
        pokeNumber: Number,
        url:String,
        // type:String
    },
    components: {
        // Pokemon
    },
    filters: {
        letterUpper: function (value) {
        let pokeName = value[0].toUpperCase() + value.slice(1);
        return pokeName;
    },
  },
}
</script>

<style scoped>
.poke-BigCard{
  width: 550px;
  /* box-shadow: 0 10px 20px 0 rgba(206, 4, 4, 0.863), 0 10px 30px 0 rgba(18, 201, 131, 0.897); */
  position: fixed;
  height:auto;
  /* align-items: center; */
}
.poke-data{
    width: 750px;
    display: flex;
    flex-wrap: wrap;
    transform:translatey(-30px);
    transform: translateX(100px);
    align-items: center;
    padding: 5px;
    /* background-color: black; */

}
.poke-data p{
    background-color:rgba(0, 0, 0, 0.07);
    border-radius: 10px;
    width: 100px;
    text-align: center;
    /* display: flex; */
}
.data{
    flex-direction: column;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 100px;
    margin-right: 30px;
}
.photo{
    image-rendering: -moz-crisp-edges;
    image-rendering: -webkit-crisp-edges;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    max-width: 60%;
    transform:translateX(100px);
    /* background-color: brown; */
}
.data-abi{
    width: 400px;
    margin-right: 5px;
}

</style>