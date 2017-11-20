<template lang="pug">
  .switcher-container
    button.switcher(v-on:click="isChart=!isChart", v-bind:class="{ active: isChart }") Chart
    button.switcher(v-on:click="isTable=!isTable", v-bind:class="{ active: isTable }") Table
</template>

<script>
export default {
  data () {
    return {
      isTable: false,
      isChart: true
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
    background-color: #8acdd6;
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