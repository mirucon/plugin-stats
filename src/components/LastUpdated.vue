<template lang="pug">
  div.last-update Last update: {{ relTime }}
</template>

<script>
import timeago from 'timeago.js'

export default {
  props: {
    lastModified: String
  },
  data () {
    return {
      relTime: ''
    }
  },
  created: function () {
    this.getTimeAgo()
  },
  methods: {
    getTimeAgo () {
      var dateArray = this.lastModified.split(',')
      dateArray[1] = dateArray[1] - 1
      var lastModified = new Date(Date.UTC(dateArray[0], dateArray[1], dateArray[2], dateArray[3], dateArray[4]))
      this.relTime = timeago().format(lastModified)
      // console.log(dateArray[0], dateArray[1], dateArray[2], dateArray[3], dateArray[4])
      // console.log(lastModified)
    }
  },
  watch: {
    lastModified: function () {
      this.getTimeAgo()
    }
  }
}
</script>

<style scoped>

</style>
