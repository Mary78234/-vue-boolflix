<template>
  <div>
    <ul class="list-group">
      <li class="list-group-item"> {{card.title || card.name}} </li>
      <li class="list-group-item"> {{card.original_title || card.original_name}} </li>
      <li class="list-group-item">
        <span v-if="getFlags(card.original_language)">
        </span>
        <span v-else-if="imageUrl === ''">{{card.original_language}} </span>
        <img v-else-if="imageUrl !== ''" :src="imageUrl" alt="">
      </li>
      <li class="list-group-item"> {{card.vote_average}} </li>
      <li class="list-group-item"> ------------------------------ </li>
    </ul>
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
      imageUrl: '',
      flagPosition: -1 //posizione bandiera corrispondete
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
        //console.log('bandiera c\'è ', flagToSearch);

        this.imageUrl = 'https://www.countryflags.io/'+this.countryFlags[this.flagPosition]+'/flat/24.png';
        
      }
      console.log('link img',flagToSearch,this.imageUrl);

    }
  }
  
}
</script>

<style lang="scss" scoped>

</style>