<template lang="pug">
  h2 {{ title }}
</template>

<script>
export default {
  props: {
    data: Object,
    kind: String,
    title: String
  },
  data () {
    return {
      total: '',
      percents: ''
    }
  },
  methods: {
    getChartData () {
      var total = 0
      var val

      for (var key in this.data) {
        val = this.data[key]
        total += val
      }
      this.total = total
    }
  },
  watch: {
    data: function () {
      this.getChartData()
    }
  }
}
</script>