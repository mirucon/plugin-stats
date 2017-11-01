<script>
import { Pie, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins

export default {
  extends: Pie,
  mixins: [reactiveProp],
  props: {
    chartData: Object
  },
  mounted: function () {
    this.renderChart(this.chartData)
  }
}
</script>