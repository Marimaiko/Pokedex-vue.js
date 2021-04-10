<template>
    <div class="big-card" >
        <b-card :img-src="image" img-alt="Card image" img-bottom>
            <b-card-text class="bigCard-title">
                <h5>Selecione um pokemon para ver suas informações!</h5>
            </b-card-text>
        </b-card>
    </div>
</template>

<script>
import image from "../assets/pokeball-icon.png";

export default {
  data() {
    return {
      image: image,
    };
  },
  props:{
    //   showCard:Boolean
  }

};
</script>

<style scoped>
.big-card{
  width: auto;
  box-shadow: 0 10px 20px 0 rgba(206, 4, 4, 0.863), 0 10px 30px 0 rgba(18, 201, 131, 0.897);
  border-radius: 35px;
  position: fixed;
}
.bigCard-title{
  text-align: center;
  margin: 20px;
  padding-top: 20px;
  margin: 20px;
}

</style>