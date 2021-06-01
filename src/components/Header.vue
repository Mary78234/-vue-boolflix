<template>
  <header>

    <!-- /container -->
    <div class="container d-flex justify-content-between align-items-center py-4">

      <h1 class="text-uppercase">Boolflix</h1>

      <!-- casella di testo da cui viene passata il titolo da cercare -->
      <input type="text" 
        v-model.trim="searchText"
        placeholder="Inserire Film da cercare"
        @keyup.enter="sendEmit('all')"
        class="form-control float-end">

      <!-- bottoni che permettono la ricerca di solo film/serie tv o entrambi -->
      <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-secondary" @click="sendEmit('movie')">Cerca Film</button>
        <button type="button" class="btn btn-secondary" @click="sendEmit('tv')">Cerca Serie TV</button>
        <button type="button" class="btn btn-secondary" @click="sendEmit('all')">Cerca entrambi</button>
      </div>

    </div>
    <!-- /container -->
    
  </header>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
      searchText: ''
    }
  },
  methods:{
    sendEmit(type){//invia tipo e titolo film da cercare al genitore
      this.$emit('startSearch', {text:this.searchText, type:type})
    }
  }
}
</script>

<style lang="scss" scoped>

  h1{
    font-weight: 700;
  }
  
  input{
    width: 300px;
  }

</style>