<script>
import { Pie, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins

export default {
  extends: Pie,
  mixins: [reactiveProp],
  props: {
    chartData: Object,
    options: Object
  },
  mounted: function () {
    this.renderChart(this.chartData, this.options)
  },
  watch: {
    options: function () {
      console.log(this.options)
    }
  }
}
</script>