<template lang="pug">
  table.table
    tr.line(v-for="(value, key) in requires")
      th.tb.key {{ key }}
      td.tb.value {{ value }}

</template>

<script>
export default {
  data () {
    return {
      labels: [],
      items: []
    }
  },
  props: {
    requires: Object
  }
}
</script>

<style lang="scss">
.table {
  margin: 0 auto;
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