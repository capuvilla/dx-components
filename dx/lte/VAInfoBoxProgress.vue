<template>
  <div :class="bgColor">
    <div class="info-box-icon">
      <q-icon :name="icon" />
    </div>
    <div class="info-box-content">
      <span class="info-box-text">{{description}}</span>
      <span class="info-box-number">{{title}}<sup style='font-size: 6pt' v-html="txtSup"></sup></span>
      <div class="progress">
        <q-linear-progress :value="calcProgress" :color="pColor" class="q-mt-xs" />
      </div>
      <span class="progress-description">
        {{progressDesc}}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InfoBoxProgress',
  props: ['color', 'icon', 'title', 'description', 'progress', 'progressDesc', 'sup', 'fontColor', 'progressColor'],
  data () {
    return {}
  },
  computed: {
    bgColor () {
      return `info-box bg-${this.color} text-${this.fontColor}`
    },
    calcProgress () {
      return this.progress / 100
    },
    txtSup () {
      return (this.sup) ? this.sup : '&nbsp;'
    },
    pColor () {
      return (this.progressColor) ? `${this.progressColor}` : 'white'
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
