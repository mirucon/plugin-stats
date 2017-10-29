<script>
import Vue from 'vue'

const PieChart = Vue.component('pie-chart', {
  props: ['req'],
  template: `
     <div>
      <h4>I am child {{req}}
      </h4>
    </div>
  `,
  mounted: function () {
    console.log(this.req)
    /*  */
  },
  watch: {
    req: function (newVal, oldVal) {
      console.log('Prop changed: ', newVal, ' | was: ', oldVal)
    }
  }
})

export default {
  PieChart
}
</script>
