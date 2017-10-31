<script>
import {Pie} from 'vue-chartjs'

export default {
  extends: Pie,
  props: ['requires', 'tested', 'requires_php'],
  mounted: function () {
    this.renderChart({
      labels: Object.keys(this.requires_php),
      datasets: [
        {label: 'My activities', backgroundColor: '#dd4b39', data: Object.values(this.requires_php)}
      ]
    }, {responsive: true, maintainAspectRatio: false})
  },
  watch: {
    requires: function (newVal, oldVal) {
      console.log('Prop changed: ', newVal, ' | was: ', oldVal)
    }
  }
}
</script>