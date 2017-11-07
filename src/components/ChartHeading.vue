<template lang="pug">
  h2 {{ total }}
</template>

<script>
export default {
  props: {
    data: Object
  },
  data () {
    return {
      total: '',
      num: '',
      percents: '',
      msg: 'hi'
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