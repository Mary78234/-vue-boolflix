<template>
  <header>

    <!-- /container -->
    <div class="container">

      <input type="text" 
        v-model.trim="searchText"
        placeholder="Inserire Film da cercare"
        class="form-control">
      <button
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
      </button>

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
  input{
    width: 300px;
  }
</style>