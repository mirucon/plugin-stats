<template lang="pug">
  #app
    pie-chart.chart.wpver(:width="300", :height="300", :chart-data="chartData")
    pie-chart.chart.wptest(:width="300", :height="300", :chart-data="chartDataTes")
    pie-chart.chart.phpver(:width="300", :height="300", :chart-data="chartDataRqp")
</template>

<script>
import axios from 'axios'
import PieChart from './components/PieChart'

export default {
  components: {
    PieChart
  },
  data () {
    return {
      requires: {},
      tested: {},
      requires_php: {},
      chartData: {},
      chartDataTes: {},
      chartDataRqp: {},
      errors: [],
      url: 'https://raw.githubusercontent.com/Mirucon/plugin-stats/master/plugins.min.json'
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
  },
  methods: {
    fillData () {
      this.chartData = {
        labels: Object.keys(this.requires),
        datasets: [
          {
            label: 'What version of WordPress requires?',
            backgroundColor: '#444444',
            borderWidth: 0.4,
            data: Object.values(this.requires)
          }
        ]
      }
    },
    fillDataTes () {
      this.chartDataTes = {
        labels: Object.keys(this.tested),
        datasets: [
          {
            label: 'On what version of WordPress tested?',
            backgroundColor: '#444444',
            borderWidth: 0.4,
            data: Object.values(this.tested)
          }
        ]
      }
    },
    fillDataRqp () {
      this.chartDataRqp = {
        labels: Object.keys(this.requires_php),
        datasets: [
          {
            label: 'What version of PHP requires?',
            backgroundColor: '#444444',
            borderWidth: 0.4,
            data: Object.values(this.requires_php)
          }
        ]
      }
    }
  },
  watch: {
    requires: function () {
      this.fillData()
    },
    tested: function () {
      this.fillDataTes()
    },
    requires_php: function () {
      this.fillDataRqp()
    }
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