<template>
  <main>
    <h1>Lista film</h1>
    <input type="text" 
      v-model.trim="searchText"
      placeholder="Inserire Film da cercare"
    >
    <button @click="$emit('startSearchFilm', searchText)">
      Cerca Film
    </button>
    <button  @click="$emit('startSearchTv', searchText)">
      Cerca Serie TV
    </button>

    <ul
      
      v-for="(value, id) in filteredList"
      :key="id"
    >
      <li>---------------Film-----------------</li>
      <li>Titolo: {{value.title}} </li>
      <li>Titolo originale: {{value.original_title}} </li>
      <li>Lingua: {{value.original_language}} </li>
      <li>Voto: {{value.vote_average}} </li>
      <li>--------------------------------------</li>
      
    </ul>

    <!-- <ul v-show="!FilmTV" 
      v-for="(value, id) in filteredList"
      :key="id"
    >
      <li>---------------Serie TV-----------------</li>
      <li>Titolo: {{value.name}} </li>
      <li>Titolo originale: {{value.original_name}} </li>
      <li>Lingua: {{value.original_language}} </li>
      <li>Voto: {{value.vote_average}} </li>
      <li>--------------------------------------</li>
    </ul> -->

  </main>
</template>

<script>
export default {
  name: 'Main',
  props:{
    filteredList: Array
  },
  data(){
    return{
      searchText:'',
      FilmTv: true,
    }
  },
  created(){
    /* if(this.filteredList.title === undefined){
      this.FilmTv = false;
    } */
  }
}
</script>

<style lang="scss" scoped>

</style>