<template>
  <div :class="bgColor">
    <div class="inner">
      <h3 style="font-size: 48pt">{{title}}<sup style='font-size: 26px' v-html="txtSup"></sup></h3>
      <p><b>{{description}}</b></p>
    </div>
    <div class="icon">
      <q-icon :name="icon" />
    </div>
    <a href="#" :class="moreText ? 'small-box-footer' : 'hidden'" @click="moreEvent">{{moreText}} <q-icon name="arrow_right" /> </a>
  </div>
</template>

<script>
export default {
  name: 'SmallBox',
  props: ['color', 'icon', 'title', 'description', 'moreText', 'sup', 'fontColor'],
  computed: {
    bgColor () {
      return `small-box bg-${this.color} text-${this.fontColor}`
    },
    txtSup () {
      return (this.sup) ? this.sup : '&nbsp;'
    }
  },
  methods: {
    moreEvent () {
      this.$emit('more-click')
    }
  },
  data () {
    return {}
  }
}
</script>

<style scoped>
@import 'src/css/adminlte/cores.css';
@import 'src/css/adminlte/smallbox.css';
</style>
