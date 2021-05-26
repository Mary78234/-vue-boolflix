<template>
  <body>
    <div id="app">
      
      <Header />
      <Main />

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
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      apiKey: 'c2ea226cb0288d7001760b50ed3a2e3f',
      query: 'lupen',
      film: []
    }
  },
  created(){
    axios.get(this.apiURL,{
        params:{
          api_key: this.apiKey,
          query: this.query,
          language: 'it-IT'
        }
      })
      .then(resp =>{
        console.log(resp);
      })
      .catch(err => {
        console.log(err);
      })
  }/* ,
  methods:{
    searchFilm(){
      axios.get(this.apiURL,{
        params:{
          api_key: this.apiKey,
          query: this.query,
          language: 'it-IT'
        }
      })
      .then(resp =>{
        console.log(resp);
      })
      .catch(err => {
        console.log(err);
      })
    }

  } */

}
</script>

<style lang="scss">
@import 'assets/style/general.scss';
@import 'assets/style/utilities.scss';

</style>
