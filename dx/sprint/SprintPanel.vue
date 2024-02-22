<template>
  <div class="row q-col-gutter-md padding">
    <div class="col-xs-12 col-sm-12 col-md-4 col-lg-4" v-for="board in boards" :key="board.id">
      <sprint-board :caption="board.titulo" :type="board.id" @novo="newcard">
        <Container
          group-name="sprint"
          class="q-gutter-sm"
          @drag-start="handleDragStart(board.id, $event)"
          @drop="handleDrop(board.id, $event)"
          :get-child-payload="getChildPayload"
          :drop-placeholder="{ className: 'placeholder' }"
        >
          <Draggable v-for="card in board.cards" :key="card.id">
            <sprint-card
              v-bind="card"
            />
          </Draggable>
        </Container>
      </sprint-board>
    </div>
  </div>
</template>

<script>
import { defineComponent, defineAsyncComponent, ref } from 'vue'
import { Container, Draggable } from 'vue3-smooth-dnd'

export default defineComponent({
  name: 'CptSprintPanel',
  components: {
    SprintCard: defineAsyncComponent(() => import('src/components/dx/sprint/SprintCard.vue')),
    SprintBoard: defineAsyncComponent(() => import('src/components/dx/sprint/SprintBoard.vue')),
    Container,
    Draggable
  },
  props: {
    boards: {
      type: [Object, Array]
    }
  },
  setup (props, { attrs, emit }) {
    const draggingCard = ref({
      lane: '',
      index: -1,
      cardData: {}
    })

    const handleDragStart = (lane, dragResult) => {
      const { payload, isSource } = dragResult
      if (isSource) {
        draggingCard.value = {
          lane,
          index: payload.index,
          cardData: {
            ...boardsInt.value[lane].cards[payload.index]
          }
        }
      }
    }
    const getChildPayload = (index) => {
      return { index }
    }
    const handleDrop = (lane, dropResult) => {
      const { removedIndex, addedIndex } = dropResult
      if (lane === draggingCard.value.lane && removedIndex === addedIndex) { return }
      if (removedIndex !== null) { boardsInt.value[lane].cards.splice(removedIndex, 1) }
      if (addedIndex !== null) { boardsInt.value[lane].cards.splice(addedIndex, 0, draggingCard.value.cardData) }
    }

    const boardsInt = ref({
      b01: {
        titulo: 'To Do',
        name: 'afazer',
        id: 'b01',
        cards: [
          {
            id: 1,
            title: 'Criar regra....',
            date: '30/01/2024',
            expired: false,
            fclist: true,
            fccomments: true,
            sizeDays: '3'
          }
        ]
      },
      b02: {
        titulo: 'In Progress',
        name: 'fazendo',
        id: 'b02',
        cards: [
          {
            id: 2,
            title: 'Contar quantidade de naps na topologia selecionada pelo usuário.',
            date: '25/01/2024',
            expired: false,
            fclist: true,
            fccomments: true,
            sizeDays: '3'
          }
        ]
      },
      b03: {
        titulo: 'Done',
        name: 'feito',
        id: 'b03',
        cards: []
      }
    })

    return {
      boardsInt,
      draggingCard,
      handleDragStart,
      handleDrop,
      getChildPayload
    }
  }
})
</script>

<style>
.scroll-area {
  width: 100%;
  height: calc(100vh - 5.5rem);
}
</style>
