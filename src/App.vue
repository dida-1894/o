<template>
  <div id="app">
    <tableData/>
  </div>
</template>

<script>
import tableData from './components/tableData'

export default {
  name: 'App',
  components: {
    tableData
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
