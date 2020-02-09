<template>
  <div id="app">
    <index-component />
  </div>
</template>

<script>
import IndexComponent from './components/IndexComponent'

export default {
  name: 'App',
  components: {
    IndexComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  overflow: hidden;
}

* {
  box-sizing: border-box;
}

td, th {
  vertical-align: middle !important;
  text-align: left!important;
}

th:nth-child(1) {
  width: 35%;
}
th:nth-child(2) {
  width: 35%;
}
th:nth-child(3) {
  width: 30%;
}
</style>
