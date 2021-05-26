<template>
  <main>
    <h1>Lista film</h1>
    <input type="text" placeholder="Inserire Film da cercare">
    <button>Cerca</button>

    <ul>
      <li></li>
    </ul>

  </main>
</template>

<script>
export default {
  name: 'Main',
  props:{
    film: Array
  }
}
</script>

<style lang="scss" scoped>

</style>