<template lang="pug">
  #app
    switcher

    h1 Plugin Stats
    p This is an unofficial stats for the plugins that are available in the WordPress.org plugin repository.
    p There are currently <strong>{{ total }}</strong> plugins in the repo.

    chart-heading.heading-wpver(:data="requires", kind="req", title="Required WordPress Version") 
    pie-chart.chart.wpver(:width="300", :height="300", :chart-data="chartData", :options="options")

    chart-heading.heading-wptest(:data="tested", kind="tes", title="Tested WordPress Version") 
    pie-chart.chart.wptest(:width="300", :height="300", :chart-data="chartDataTes", :options="options")

    chart-heading.heading-phpver(:data="requires_php" kind="rqp", title="Required PHP Version")
    pie-chart.chart.phpver(:width="300", :height="300", :chart-data="chartDataRqp", :options="options")

    chart-heading.heading-dl(:data="downloads", kind="dl", title="Downloads")
    pie-chart.chart.dl(:width="300", :height="300", :chart-data="chartDataDl", :options="options")

    chart-heading.heading-ins(:data="installs", kind="ins", title="Active Installs") 
    pie-chart.chart.ins(:width="300", :height="300", :chart-data="chartDataIns", :options="options")

    chart-heading.heading-dates(:data="dates", kind="dates", title="Last update") 
    pie-chart.chart.dates(:width="300", :height="300", :chart-data="chartDataDates", :options="options")

    footer.footer
      p.copyright &copy; 2017 Mirucon
</template>

<script>
import axios from 'axios'
import PieChart from './components/PieChart'
import ChartHeading from './components/ChartHeading'
import Switcher from './components/Switcher'
import palette from 'google-palette'

export default {
  components: {
    PieChart,
    ChartHeading,
    Switcher
  },
  data () {
    return {
      requires: {},
      tested: {},
      requires_php: {},
      downloads: {},
      installs: {},
      dates: {},
      total: '',
      chartData: {},
      chartDataTes: {},
      chartDataRqp: {},
      chartDataDl: {},
      chartDataIns: {},
      chartDataDates: {},
      options: {responsive: true, maintainAspectRatio: true},
      colors: [],
      errors: [],
      url: 'https://raw.githubusercontent.com/Mirucon/plugin-stats-backend/json/plugins.min.json'
    }
  },
  created: function () {
    axios.get(this.url)
    .then(response => {
      this.requires = response.data[0]
      this.tested = response.data[1]
      this.requires_php = response.data[2]
      this.downloads = response.data[3]
      this.installs = response.data[4]
      this.dates = response.data[5]
      this.total = response.data[6]
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
            label: 'Versions that plugins requires',
            backgroundColor: palette('tol-sq', Object.keys(this.requires).length).map(function (hex) {
              return '#' + hex
            }),
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
            label: 'Versions that plugins tested',
            backgroundColor: palette('tol-sq', Object.keys(this.tested).length).map(function (hex) {
              return '#' + hex
            }),
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
            label: 'PHP Versions that plugins requires',
            backgroundColor: palette('tol-sq', Object.keys(this.requires_php).length).map(function (hex) {
              return '#' + hex
            }),
            borderWidth: 0.4,
            data: Object.values(this.requires_php)
          }
        ]
      }
    },
    fillDataDl () {
      this.chartDataDl = {
        labels: Object.keys(this.downloads),
        datasets: [
          {
            label: 'Number of Downloads',
            backgroundColor: palette('tol-sq', Object.keys(this.downloads).length).map(function (hex) {
              return '#' + hex
            }),
            borderWidth: 0.4,
            data: Object.values(this.downloads)
          }
        ]
      }
    },
    fillDataIns () {
      this.chartDataIns = {
        labels: Object.keys(this.installs),
        datasets: [
          {
            label: 'Number of Active Installs',
            backgroundColor: palette('tol-sq', Object.keys(this.installs).length).map(function (hex) {
              return '#' + hex
            }),
            borderWidth: 0.4,
            data: Object.values(this.installs)
          }
        ]
      }
    },
    fillDataDates () {
      this.chartDataDates = {
        labels: Object.keys(this.dates),
        datasets: [
          {
            label: 'The last updates',
            backgroundColor: palette('tol-sq', Object.keys(this.dates).length).map(function (hex) {
              return '#' + hex
            }),
            borderWidth: 0.4,
            data: Object.values(this.dates)
          }
        ]
      }
    }
  },
  mounted: function () {
    this.options.tooltips = {
      callbacks: {
        label: function (tooltipItem, data) {
          var label = data.labels[tooltipItem.index]
          var dataset = data.datasets[tooltipItem.datasetIndex]
          var total = dataset.data.reduce(function (previousValue, currentValue, currentIndex, array) {
            return previousValue + currentValue
          })
          var currentValue = dataset.data[tooltipItem.index]
          var percentage = (((currentValue / total) * 100) + 0.5).toFixed(1)
          return ' ' + label + ': ' + percentage + '%, ' + currentValue
        }
      },
      bodyFontSize: 14
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
    },
    downloads: function () {
      this.fillDataDl()
    },
    installs: function () {
      this.fillDataIns()
    },
    dates: function () {
      this.fillDataDates()
    }
  }
}
</script>

<style lang="scss">
#app {
  max-width: 800px;
  margin: 20px auto 0;
  color: #2c3e50;
  text-align: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
h2 {
  margin: 1.4em 0 .3em;
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
.chart {
  margin-bottom: 1.6em
}
</style>