<template>
  <header>

    <!-- /container -->
    <div class="container">

      <h1>Boolflix</h1>
      <input type="text" 
        v-model.trim="searchText"
        placeholder="Inserire Film da cercare"
        @keyup.enter="sendEmit('all')"
        class="form-control">
      <!-- <button
      @click="sendEmit('movie')">
        Cerca Film
      </button>
      <button
      @click="sendEmit('tv')">
        Cerca Serie TV
      </button>
      <button
      @click="sendEmit('all')">
        Cerca Serie TV
      </button> -->

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
    sendEmit(type){//invia tipo e titolo film da cercare
      this.$emit('startSearch', {text:this.searchText, type:type})
    }
  }
}
</script>

<style lang="scss" scoped>
  .container{
    display: flex;
    justify-content: space-between;
    height: 100%;
  }
  h1{
    font-weight: 700;
    text-transform: uppercase;
  }

  input{
    width: 300px;
    height: 30px;
    padding: 0 10px
  }
</style>