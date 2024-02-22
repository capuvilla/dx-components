<template>
  <q-card style="border-radius: 15px;" class="shadow-6 mycard cursor-pointer" @click="onClick">
    <q-card-section horizontal>
      <div :style="`background-color: ${hexColor}; width: 0.4em; min-width: 0.4em;`"></div>
      <q-card class="full-width q-pa-sm">
        <q-card-section horizontal class="q-gutter-xl">
          <div>
            <div class="text-subtitle"><span class="text-bold">[{{ id }}]</span> {{ title }}</div>
            <div :class="`text-subtitle2 ${expired ? 'text-red' : ''}`">{{ date }}</div>
            <div v-if="sizeDays">{{ `Tamanho ${qtdDias} ${ (qtdDias === '1' ? 'dia' : 'dias')}` }}</div>
            <div v-if="responsibleUser">{{ responsibleUser }}
              <q-tooltip v-if="responsibleEmail">{{ responsibleUser }} {{ `<${responsibleEmail}>` }}</q-tooltip>
            </div>
          </div>
        </q-card-section>
        <q-card-actions align="around" v-if="fcavatar || fclist || fccomments">
          <q-avatar size="40px" v-if="fcavatar">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png">
          </q-avatar>
          <q-space />
          <q-icon name="format_list_numbered" style="font-size: 2rem;" v-if="fclist" />
          <q-icon name="question_answer" style="font-size: 2rem;" v-if="fccomments" />
        </q-card-actions>
      </q-card>
    </q-card-section>
  </q-card>
</template>

<script>
import { ref, watch } from 'vue'
import { useQuasar } from 'quasar'

export default {
  name: 'CptSprintCard',
  props: {
    id: {
      type: Number,
      default: null
    },
    title: {
      type: String,
      default: ''
    },
    responsibleUser: {
      type: String,
      default: null
    },
    responsibleEmail: {
      type: String,
      default: null
    },
    sizeDays: {
      type: Number,
      default: null
    },
    expired: {
      type: Boolean,
      default: false
    },
    executed: {
      type: Boolean,
      default: false
    },
    fcavatar: {
      type: Boolean,
      default: false
    },
    fclist: {
      type: Boolean,
      default: false
    },
    fccomments: {
      type: Boolean,
      default: false
    },
    color: {
      type: String,
      default: '#643b8c'
    },
    date: {
      type: String,
      default: ''
    }
  },
  setup (props, { attrs, emit }) {
    const $q = useQuasar()
    const hexColor = ref(props.color)
    const ctlCheck = ref(props.executed)
    const qtdDias = ref(props.sizeDays)

    const onClick = async () => {
      emit('click', props.id)
    }

    const onClickCheck = async () => {
      $q.dialog({
        title: 'Tarefa concluida?',
        cancel: {
          label: 'Não',
          flat: true
        },
        persistent: true,
        ok: {
          label: 'Sim',
          flat: true
        }
      }).onOk(() => {
        ctlCheck.value = true
      }).onCancel(() => {
        ctlCheck.value = false
      })
    }

    watch(() => props.sizeDays, (newValue) => {
      console.log(newValue)
      qtdDias.value = newValue
    })

    return {
      hexColor,
      ctlCheck,
      qtdDias,
      onClick,
      onClickCheck
    }
  }
}
</script>

<style>
.mycard {
  border-radius: 0.4rem;
  box-shadow: 0 2px 0 rgba(9, 30, 66, 0.25);
}

.shadow-box {
  border-radius: 50%;
  font-size: 2.5em;
  box-shadow: 0 6px 6px rgba(182, 182, 182, 0.75);
  -moz-box-shadow:0 6px 6px rgba(182, 182, 182, 0.75);
  -webkit-box-shadow: 0 6px 6px rgba(182, 182, 182, 0.75);
}

.my-picker {
  max-width: 250px
}
</style>
