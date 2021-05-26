<template>
  <body>
    <div id="app">
      
      <Header />
      <Main 
        @startSearchFilm="startSearchFilm"
        @startSearchTv="startSearchTv"
        :filteredList='filteredList'
      />

    </div>
  </body>
</template>

<script>
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
      axios,
      apiURLmovie: 'https://api.themoviedb.org/3/search/movie',
      apiURLtv: 'https://api.themoviedb.org/3/search/tv',
      apiKey: 'c2ea226cb0288d7001760b50ed3a2e3f',
      query: '',
      List: []
    }
  },
  computed:{
    filteredList(){
      return this.List;
    }
  },
  created(){

  },
  methods:{
    startSearchFilm(filmToSearch){
      this.query = filmToSearch;
      if(this.query !== ''){
        axios.get(this.apiURLmovie,{
          params:{
            api_key: this.apiKey,
            query: this.query,
            language: 'it-IT'
          }
        })
        .then(resp =>{
          this.List = resp.data.results;
          console.log(this.List);
        })
        .catch(err => {
          console.log(err);
        })
      }
    },
    startSearchTv(TvToSearch){
      this.query = TvToSearch;
      if(this.query !== ''){
        axios.get(this.apiURLtv,{
          params:{
            api_key: this.apiKey,
            query: this.query,
            language: 'it-IT'
          }
        })
        .then(resp =>{
          this.List = resp.data.results;
          console.log(this.List);
        })
        .catch(err => {
          console.log(err);
        })
      }
    },
    /* startSearch(){
      axios.get(this.apiURL,{
        params:{
          api_key: this.apiKey,
          query: this.query,
          language: 'it-IT'
        }
      })
      .then(resp =>{
        this.List = resp.data.results;
        console.log(this.List);
      })
      .catch(err => {
        console.log(err);
      })
    } */

  }

}
</script>

<style lang="scss">
@import 'assets/style/general.scss';
@import 'assets/style/utilities.scss';

</style>
