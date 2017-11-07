<script>
import { Pie, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins

export default {
  data () {
    return {
      options: {responsive: true, maintainAspectRatio: true}
    }
  },
  extends: Pie,
  mixins: [reactiveProp],
  props: {
    chartData: Object
  },
  mounted: function () {
    this.renderChart(this.chartData, this.options)
  }
}
</script>