<template lang="pug">
  #app
    pie-chart(:width="400", :height="400", :requires="requires")
    pie-chart(:tested="tested")
    pie-chart(:width="600", :height="600", :requires_php="requires_php")
</template>

<script>
import axios from 'axios'
import PieChart from './components/PieChart'
import {Pie} from 'vue-chartjs'

export default {
  components: {
    PieChart
  },
  data () {
    return {
      requires: [],
      tested: [],
      requires_php: [],
      errors: [],
      url: 'https://api.miruc.co/plugins.min.json',
      test: 'test'
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
}
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