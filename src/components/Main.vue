<template>
  <main class="container">
  
    <h1> {{titles[type]}} </h1>

    <Card 
    v-for="card in list"
    :key="card.id"
    :card="card"/>

  </main>
</template>

<script>
import Card from './Card.vue';
export default {
  name: 'Main',
  components:{
    Card
  },
  props:{
    type: String,
    list: Array
  },
  data(){
    return{
      titles:{
        'movie': 'Film trovati',
        'tv': 'Serie tv trovate'
      }
    }
  },
  created(){
    
  }
}
</script>

<style lang="scss" scoped>
  main.container{
    background-color: bisque;
  }

</style>