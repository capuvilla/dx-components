<template>
  <div :class="bgColor">
    <span :class="bgColorIcon"><q-icon :name="icon" /></span>

    <div class="info-box-content">
      <span :class="textColorDesc">{{description}}</span>
      <span :class="textColorTitle" style="font-size: 20pt">{{title}}<sup style='font-size: 8pt' v-html="txtSup"></sup></span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InfoBox',
  props: ['color', 'icon', 'title', 'description', 'bgicon', 'fontcolor', 'sup'],
  data () {
    return {}
  },
  computed: {
    bgColor () {
      return `info-box bg-${this.color}`
    },
    bgColorIcon () {
      return `info-box-icon bg-${this.bgicon}`
    },
    textColorDesc () {
      return `info-box-text text-${this.fontcolor}`
    },
    textColorTitle () {
      return `info-box-number text-${this.fontcolor}`
    },
    txtSup () {
      return (this.sup) ? this.sup : '&nbsp;'
    }
  },
  methods: {
    moreEvent () {
      this.$emit('more-click')
    }
  }
}
</script>

<style scoped>
@import 'src/css/adminlte/cores.css';
@import 'src/css/adminlte/infobox.css';
</style>
