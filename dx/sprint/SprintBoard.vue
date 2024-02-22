<template>
  <q-card style="border-radius: 15px;">
    <q-card-actions>
      <q-toolbar>
        <q-toolbar-title class="text-subtitle1">
          {{ caption }}
        </q-toolbar-title>
        <q-btn dense round color="primary" icon="add" @click="onNew" />
      </q-toolbar>
    </q-card-actions>
    <q-card-section>
      <div class="q-gutter-sm">
        <slot />
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
// import { ref, watch } from 'vue'
// import { useQuasar } from 'quasar'

export default {
  name: 'CptSprintBoard',
  props: {
    caption: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: ''
    }
  },
  setup (props, { attrs, emit }) {
    const onNew = async () => {
      emit('new', props.type)
    }
    return {
      onNew
    }
  }
}
</script>

<style scoped>
.myBoard {
  border-radius: 0.4rem;
  box-shadow: 0 2px 0 rgba(9, 30, 66, 0.25);
}
</style>
