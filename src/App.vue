<template lang="pug">
  #app

    pie-chart
</template>

<script>
import axios from 'axios'
import Vue from 'vue'
import PieChart from './components/PieChart'
import {Pie} from 'vue-chartjs'

console.clear()

const App = new Vue({
  el: '#app',
  components: {
    PieChart
  },
  data () {
    return {
      requires: [],
      tested: [],
      requires_php: [],
      errors: [],
      url: 'https://api.miruc.co/plugins.min.json'
    }
  },
  created: function () {
    axios.get(this.url)
    .then(response => {
      this.requires = response.data[0]
      this.tested = response.data[1]
      this.requires_php = response.data[2]
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
})
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
