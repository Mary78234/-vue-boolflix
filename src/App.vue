<template>
  <body>
    <div id="app">
      
      <Header @startSearch="startSearch"/>

      <div class="container">
        <h1 v-if="results.movie.length === 0 && results.tv.length === 0 ">
          Nessun risultato trovato
        </h1>

        <Main 
        v-if="results.movie.length > 0" 
        type="movie"
        :list="results.movie"/>

        <Main
        v-if="results.tv.length > 0" 
        type="tv" 
        :list="results.tv"/>

      </div>

      

    </div>
  </body>
</template>

<script>
/* <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" integrity="sha512-iBBXm8fW90+nuLcSKlbmrPcLa0OT92xO1BIsZ+ywDWZCvqsWgccV3gFoRBv0z+8dLJgyAHIhR35VZc2oM/gI1w==" crossorigin="anonymous" referrerpolicy="no-referrer" /> */
import axios from 'axios';
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data(){
    return{
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: 'c2ea226cb0288d7001760b50ed3a2e3f',
      results:{//results saved here
        'movie':[],
        'tv':[]
      }
    }
  },
  /* created(){

  }, */
  methods:{
    startSearch(obj){ 
      this.resetResults(); //reset old results

      if(obj.type === 'all'){
        this.getAPI(obj.text, 'movie');
        this.getAPI(obj.text, 'tv');
      }else{
        this.getAPI(obj.text, obj.type);
      }

    },

    resetResults(){
      this.results.movie = [];
      this.results.tv = [];
    },

    getAPI(query, type){

      if(query !== ''){
        
        axios.get(this.apiUrl+type,{
          params:{
            api_key: this.apiKey,
            query: query,
            language: 'it-IT'
          }
        })
        .then(res => {
          this.results[type] = res.data.results;
          console.log("film: ", this.results.movie);
          console.log("serie tv: ", this.results.tv);
        })
        .catch(err => {
          console.log(err);
          console.log('qui errore');
        })
      }

    }

  }

}
</script>

<style lang="scss">
@import 'assets/style/general.scss';
@import 'assets/style/utilities.scss';

</style>
