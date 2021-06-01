<template>
  <div class="flip-card ">

    <!-- flip card inner -->
    <div class="flip-card-inner">

      <div class="flip-card-front">
        <img  class="cover-img" :src="imageUrl+card.poster_path" alt="poster"><br>
        <span>Immagine non presente</span>
      </div>

      <!-- flip card back -->
      <div class="flip-card-back">
        <ul class="">

          <li class="">
            <span>Titolo: </span>
            <span>{{card.title || card.name}}</span></li>
          <li class="">Titolo originale: {{card.original_title || card.original_name}} </li>
          
          <!-- lingua con bandiera -->
          <li class="">
            lingua: 
            <span v-if="getFlags(card.original_language)">
              <img class="img-flag" :src="flagUrl" :alt="card.title || card.name">
            </span>
            <span v-else> {{card.original_language}} </span>
          </li>
          <!-- /lingua con bandiera -->

          <!-- stelle in base al punteggio -->
          <li class="">
            Voto:  
            <span v-if="starScore(card.vote_average)">
              <i class="fas fa-star" v-for="star in numStars" :key="star"></i>
              <i class="far fa-star" v-for="star in (5 - numStars)" :key="star"></i>
            </span>
            <span v-else>- non presente -</span>
          </li>
          <!-- /stelle in base al punteggio -->

          <!-- overview -->
          <li class="overflow-scroll">
            Overview: 
            <span v-show="card.overview !== ''">{{card.overview}}</span> 
            <span v-show="card.overview === ''" >- non presente -</span>
          </li>
          <!-- /overview -->


        </ul>
      </div>
      <!-- flip card back -->

    </div>
    <!-- flip card inner -->

  </div>
</template>

<script>
export default {
  name: 'Card',
  props:{
    card: Object
  },
  data(){
    return{
      flags:['it', 'en', 'fr', 'ja'], //sigla bandiera da server
      countryFlags:['it', 'gb', 'fr', 'jp'], //sigla corrispondente da sito bandiere
      flagUrl: '',
      flagPosition: -1 ,//posizione bandiera corrispondete
      imageUrl: 'https://image.tmdb.org/t/p/w342',
      seeStar: false,
      numStars: 0
    }
  },
  methods:{
    getFlags(flagToSearch){//cerco bandiera

      //se bandiera è nella lista flags con
      if(this.flags.includes(flagToSearch)){
        //ciclo per trovare la posizione della bandiera
        this.flags.forEach((flag, index) => {
          if(flag === flagToSearch){
            this.flagPosition = index;
          }
        });
        this.flagUrl = 'https://www.countryflags.io/' + this.countryFlags[this.flagPosition]+'/flat/24.png';

        return true;
      }
      /* this.flagUrl = 'https://www.countryflags.io/' + flagToSearch +'/flat/24.png'; */

      return false;

    },

    starScore(num){ //calcola le stelle su base 5 anzichè 10
      this.numStars = parseInt(num / 10 * 5);
      return this.numStars;
    }
  }
  
}
</script>

<style lang="scss" scoped>

  .fa-star{
    color: yellow;
  }

  .flip-card {
    flex-basis: calc(100% / 3 - 20px);
    height: 400px;
    margin: 10px;
    background-color: transparent;
    /* width: 320px;
    height: 420px; */
    perspective: 1000px;
  }

  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  }

  .flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
  }

  .flip-card-front, .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    overflow: scroll;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    border: 1px solid white;
  }

  .flip-card-front {
    background-color: #bbb;
    color: black;/* 
    overflow: hidden; */
    .cover-img{
      width: 100%;
    }
  }

  .flip-card-back {
    background-color: black;
    color: white;
    transform: rotateY(180deg);
    ul{
      text-align: left;
      margin: 20px 5px;
    }
  }

  .img-flag{
    vertical-align: middle;
  }

</style>