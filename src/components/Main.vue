<template>
  <div>
    <h1> Hello Component</h1>
    <h2> {{ msg }} </h2>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style scoped>
</style>
