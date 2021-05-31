<template>
  <div class="box"> 
    <div class="flip-card">

      <!-- flip card inner -->
      <div class="flip-card-inner">

        <div class="flip-card-front">
          <img class="cover-img" :src="imageUrl+card.poster_path" alt="">
        </div>

        <!-- flip card back -->
        <div class="flip-card-back">
            <ul class="list-group">

              <li class="list-group-item">Titolo: {{card.title || card.name}} </li>
              <li class="list-group-item">Titolo originale: {{card.original_title || card.original_name}} </li>
              <li class="list-group-item">
                <span v-if="getFlags(card.original_language)">
                  Language: <img class="img-flag" :src="flagUrl" alt="">
                </span>
                <span v-else>Language: {{card.original_language}} </span>
              </li>
              <li class="list-group-item">
                Voto:  
                <span v-if="starScore(card.vote_average)">
                  <i class="fas fa-star"
                  v-for="star in numStars" :key="star"></i>
                </span>
                <span v-else> not scored </span>
              </li>

            </ul>
        </div>
        <!-- flip card back -->

      </div>
      <!-- flip card inner -->

    </div>
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
      flags:['it', 'en', 'fr'], //sigla bandiera da server
      countryFlags:['it', 'gb', 'fr'], //sigla corrispondente da sito bandiere
      flagUrl: '',
      flagPosition: -1 ,//posizione bandiera corrispondete
      imageUrl: 'https://image.tmdb.org/t/p/w342',
      seeStar: false,
      numStars: 0
    }
  },
  methods:{
    getFlags(flagToSearch){//cerco bandiera
      //se bandiera è nella lista flags
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
    margin: 10px;
    background-color: transparent;
    width: 300px;
    height: 400px;
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
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    border: 1px solid white;
  }

  .flip-card-front {
    background-color: #bbb;
    color: black;
    overflow: hidden;
    .cover-img{
      width: 100%;
    }
  }

  .flip-card-back {
    background-color: black;
    color: white;
    transform: rotateY(180deg);
    margin: 80px 20x;
  }

</style>