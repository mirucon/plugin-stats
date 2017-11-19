<template lang="pug">
  .switcher-container
    button.switcher(v-on:click="table", v-bind:class="{ active: isTable }") Table
    button.switcher(v-on:click="chart", v-bind:class="{ active: isChart }") Chart
</template>

<script>
export default {
  data () {
    return {
      isTable: false,
      isChart: true
    }
  },
  methods: {
    table () {
      this.isTable = !this.isTable
      this.isChart = false
    },
    chart () {
      this.isChart = !this.isChart
      this.isTable = false
    }
  }
}
</script>

<style lang="scss">
.switcher {
  display: inline-block;
  padding: .8em .9em;
  border: none;
  background: #ececec;
  color: #00BCD4;
  font-size: .8em;
  text-align: right;
  border-radius: 2px;
  text-transform: uppercase;
  font-weight: 600;
  -webkit-appearance: none;
  -moz-appearance: none;
  transition: .2s;
  &:hover {
    color: #fafafa;
    background-color: #97c5dc;
    outline: none;
  }
  &:focus {
    outline: none;
  }
  &:not(:last-child) {
    margin-right: 1px;
  }
}
.active {
  @extend .switcher:hover;
  background-color: #39c;
  &:hover {
    background-color: #39c;
  }
}
</style>