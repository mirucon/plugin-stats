<template lang="pug">
  .table-container
    .table
      div.keys
        span.tb.key(v-for="key in keysFirstHalf") {{ key }}
      div.values
        span.tb.value(v-for="value in valuesFirstHalf") {{ value }}
    .table(v-if="isHalf")
      div.keys
        span.tb.key(v-for="key in keysSecoundHalf") {{ key }}
      div.values
        span.tb.value(v-for="value in valuesSecoundHalf") {{ value }}
    .table(v-if="isHalf")
      div.keys
        span.tb.key(v-for="key in keysThirdHalf") {{ key }}
      div.values
        span.tb.value(v-for="value in valuesThirdHalf") {{ value }}

</template>

<script>
export default {
  data () {
    return {
      keysFirstHalf: [],
      valuesFirstHalf: [],
      keysSecoundHalf: [],
      valuesSecoundHalf: [],
      keysThirdHalf: [],
      valuesThirdHalf: [],
      isHalf: false
    }
  },
  props: {
    tableData: Object
  },
  mounted: function () {
    this.firstHalf = this.tableData
    var dataLength = Object.keys(this.tableData).length

    var keys = Object.keys(this.tableData)
    var values = Object.values(this.tableData)

    if (dataLength > 20) {
      this.isHalf = true
      var lengthNum = Math.ceil(dataLength / 3)

      this.keysFirstHalf = keys.slice(0, lengthNum)
      this.valuesFirstHalf = values.slice(0, lengthNum)

      this.keysSecoundHalf = keys.slice(lengthNum, dataLength / 3 * 2)
      this.valuesSecoundHalf = values.slice(lengthNum, dataLength / 3 * 2)

      this.keysThirdHalf = keys.slice(Math.ceil(dataLength / 3 * 2), dataLength)
      this.valuesThirdHalf = values.slice(Math.ceil(dataLength / 3 * 2), dataLength)
    } else {
      this.keysFirstHalf = keys
      this.valuesFirstHalf = values
    }
  }
}
</script>

<style lang="scss">
.table-container {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  max-width: 440px;
  margin: 0 auto;
}
.table {
  margin: .7em auto 0;
}

.keys, .values {
  display: inline-flex;
  flex-flow: column wrap;
}
.keys {
  font-weight: 600;
}
.values {
  margin-left: .14em;
}

.key {
  background: #fcfdfc;
  border-radius: 2px;
}
.tb {
  display: inline-flex;
  box-sizing: border-box;
  justify-content: center;
  padding: .6em .7em;
  border-bottom: 1px solid #ddd;
}
</style>