<template lang="pug">
  .table-container
    table.table
      tr.line(v-for="(value, key) in firstHalf")
        th.tb.key {{ key }}
        td.tb.value {{ value }}
    table.table
      tr.line(v-for="(value, key) in secondHalf")
        th.tb.key {{ key }}
        td.tb.value {{ value }}

</template>

<script>
export default {
  data () {
    return {
      keys: [],
      values: [],
      firstHalf: {},
      secondHalf: {},
      isHalf: false
    }
  },
  props: {
    tableData: Object
  },
  methods: {
    getObject () {
      this.firstHalf = this.tableData
      var dataLength = Object.keys(this.tableData).length

      if (dataLength > 20) {
        this.isHalf = true
        var chartData = {}
        var lengthNum = Math.ceil(dataLength / 2)

        console.log('totalLength: ' + dataLength)
        console.log('lengthNum: ' + lengthNum)

        var keys = Object.keys(this.tableData)
        var values = Object.values(this.tableData)

        var keysFirstHalf = keys.slice(0, lengthNum)
        var valuesFirstHalf = values.slice(0, lengthNum)

        for (var i = 0; i < lengthNum; i++) {
          chartData[keysFirstHalf[i]] = valuesFirstHalf[i]
        }
        this.firstHalf = chartData
        chartData = {}

        var keysSecoundHalf = keys.slice(lengthNum, dataLength)
        var valuesSecoundHalf = values.slice(lengthNum, dataLength)

        for (i = 0; i < lengthNum; i++) {
          chartData[keysSecoundHalf[i]] = valuesSecoundHalf[i]
        }
        this.secondHalf = chartData

        console.log('firstHalf: ' + Object.keys(this.firstHalf).length)
      }
    }
  },
  mounted: function () {
    this.getObject()
  }
}
</script>

<style lang="scss">
.table {
  margin: .7em auto 0;
}
.line {
  border-bottom: 1px solid #ddd;
}
.tb {
  padding: .5em .6em;
  border-bottom: 1px solid #ddd;
}
.key {
  background: #fefefe;
  border-radius: 1px;
}
</style>