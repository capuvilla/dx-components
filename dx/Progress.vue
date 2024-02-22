<template>
  <span>
    <q-bar
      dense
      class="bg-transparent text-caption"
      :class="textClass"
    >
      <div>{{ title }}</div>
      <q-space />
      <div class="text-bold">{{ metric }}</div>
    </q-bar>
    <q-linear-progress :size="(activeLabel) ? '15px' : sizeLabel" :value="progress" :color="color">
      <div class="absolute-full flex flex-center itens-center" v-if="activeLabel">
        <q-badge dense :color="backgroundLabel" :text-color="colorLabel" :label="progressLabel" style="font-size: 10px;" />
      </div>
    </q-linear-progress>
  </span>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  name: 'CptProgress',
  props: {
    title: {
      type: String,
      default: ''
    },
    metric: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: 'red'
    },
    textClass: {
      type: String,
      default: ''
    },
    colorLabel: {
      type: String,
      default: 'accent'
    },
    sizeLabel: {
      type: String,
      default: '15px'
    },
    backgroundLabel: {
      type: String,
      default: 'white'
    },
    activeLabel: {
      type: [Boolean],
      default: () => false
    },
    value: {
      type: Number,
      default: 0
    }
  },
  setup (props) {
    const progress = ref(props.value)

    return {
      progress,
      progressLabel: computed(() => (progress.value * 100).toFixed(2) + '%')
    }
  }
}
</script>
