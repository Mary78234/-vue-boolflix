<template>
  <main>
  
    <h1> {{titles[type]}} </h1>
    <div class="container">
      <Card 
      v-for="card in list"
      :key="card.id"
      :card="card"/>
    </div>

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
  h1{
    margin-top: 20px;
    padding-left: 10px;
  }
  .container{
    display: flex;
    flex-wrap: wrap;
    margin-top: 10px;
  }

</style>