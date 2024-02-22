<template>
  <!-- BASIC -->
  <q-card flat bordered v-if="type === 'basic'">
    <q-bar dense class="text-caption" v-if="title">
      <q-icon v-if="icon" :name="icon" />
      <div>{{ title }}</div>
      <slot name="itnBar"></slot>
    </q-bar>
    <q-card-section>
      <slot name="itnCard">{{ text }}</slot>
    </q-card-section>

    <slot name="itnFim"></slot>
  </q-card>
  <!-- SOCIAL -->
  <q-card :class="`${cardclass}`" bordered v-if="type === 'social'">
    <q-card-section class="q-pa-none">
      <q-item :style="`background-color: ${colorBackground}`" class="q-pa-none">
        <q-item-section v-if="icon !== '' && position === 'left'" side :style="`background-color: ${colorBackground2}`"
                        class=" q-pa-lg q-mr-none text-white">
          <q-icon :name="icon" color="white" size="24px"></q-icon>
        </q-item-section>
        <q-item-section class=" q-pa-md q-ml-none text-white">
          <q-item-label class="text-white text-h6 text-weight-bolder">{{ value }}</q-item-label>
          <q-item-label>{{ title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="icon !== '' && position === 'right'" :style="`max-width: 66px; background-color: ${colorBackground2}`"
                        class=" q-pa-lg q-mr-none text-white">
          <q-icon :name="icon" color="white" size="24px"></q-icon>
        </q-item-section>
      </q-item>
    </q-card-section>
  </q-card>
  <!-- CRM -->
  <q-card :class="`${cardclass}`" bordered v-if="type === 'crm'">
    <q-card-section class="q-pa-none">
      <q-item :style="`background-color: ${colorBackground}`" class="q-pa-none">
        <q-item-section v-if="icon !== '' && position === 'left'" side class="q-pa-sm q-mr-md text-white">
          <q-icon :name="icon" color="white" size="44px"></q-icon>
        </q-item-section>
        <q-item-section class=" q-pa-md q-ml-none text-white">
          <q-item-label class="text-white text-h6 text-weight-bolder">{{ value }}</q-item-label>
          <q-item-label>{{ title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="icon !== '' && position === 'right'" side class="q-mr-md text-white">
          <q-icon :name="icon" color="white" size="44px"></q-icon>
        </q-item-section>
      </q-item>
    </q-card-section>
  </q-card>
  <!-- CRM 2 -->
  <q-card :class="`${cardclass}`" bordered v-if="type === 'crm2'">
    <q-card-section class="q-pa-none">
      <q-item :style="`background-color: ${colorBackground}`" class="q-pa-none">
        <q-item-section v-if="icon !== '' && position === 'left'" side class="q-pa-sm q-mr-md text-white">
          <q-icon :name="icon" color="black" size="44px"></q-icon>
        </q-item-section>
        <q-item-section class=" q-pa-md q-ml-none text-white">
          <q-item-label class="text-black text-h6 text-weight-bolder">{{ value }}</q-item-label>
          <q-item-label class="text-black">{{ title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="icon !== '' && position === 'right'" side class="q-mr-md text-white">
          <q-icon :name="icon" color="black" size="44px"></q-icon>
        </q-item-section>
      </q-item>
    </q-card-section>
  </q-card>
  <!-- Grow -->
  <q-card flat class="q-pa-none" :class="cardClass" v-if="type === 'grow'">
    <q-card-section class="q-pa-none">
      <q-item :style="`background-color: ${colorBackground}`" class="q-pa-none">
        <q-item-section
          v-if="icon !== '' && position === 'left'"
          side
          class="q-mr-none"
          style="margin-left: 15px"
        >
        <q-icon :name="icon" :class="colorText" size="50px"></q-icon>
        </q-item-section>
        <q-item-section class="q-pl-md">
          <q-item-label class="text-h6 text-weight-bolder" :class="`${colorText}`">{{ value }}</q-item-label>
          <q-item-label :class="`${colorText}`">{{ title }}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="icon !== '' && position === 'right'"
          side
          class="q-mr-none"
          style="margin-right: 10px"
        >
          <q-icon :name="icon" :class="colorText" size="50px"></q-icon>
        </q-item-section>
      </q-item>
    </q-card-section>
    <div :class="classBar" style="height: 5px"></div>
  </q-card>
  <!-- CAFE -->
  <q-card class="no-shadow" bordered v-if="type === 'cafe'">
    <q-img :src="imgbackground"/>
    <q-card-section class="absolute absolute-center text-center">
      <q-avatar size="100px" class="shadow-10">
        <img :src="avatar">
      </q-avatar>
    </q-card-section>
    <q-card-section class="q-pt-none q-mt-xl">
      <div class="text-subtitle1">
        {{ title }}
      </div>
      <div class="text-caption text-grey">
        {{ text }}
      </div>
    </q-card-section>
    <q-separator/>
    <slot name="cardAction"></slot>
  </q-card>
  <!-- infobox CA -->
  <q-card
    v-if="type === 'infobox'"
    bordered
    flat
    :class="classCard"
    :style="`background-color: ${colorBackground}; color: ${colorText}`"
  >
    <div
      class="infoBox"
      :class="`text-${position}`"
    >{{ title }}</div>
    <div :class="classValue">{{ value }}</div>
  </q-card>
  <!-- infobox COM ASSUNTO CA -->
  <q-card
    bordered
    flat
    class="q-pa-xs col-xs-12 col-sm-12 col-md"
    v-if="type === 'infobox2'"
  >
    <q-card-section class="row q-pa-none q-py-xs q-gutter-xs items-center">
      <label class="text-subtitle2 q-pr-sm">{{ text }}</label>
      <q-separator vertical />
      <q-card
        bordered
        flat
        v-for="vlr in dds" :key="vlr.title"
        class="q-px-xs col-xs-12 col-sm-12 col-md infoBox"
        :style="`background-color: ${vlr.colorBackground}; color: ${vlr.colorText}`"
      >
        <div
          class="infoBox"
          :class="`text-${vlr.position}`"
        >{{ vlr.title }}</div>
        <div :class="vlr.classValue">{{ vlr.value }}</div>
      </q-card>
    </q-card-section>
  </q-card>
  <!-- infobox 3 CA -->
  <q-card
    v-if="type === 'infobox3'"
    :bordered="bordered"
    flat
    class="q-px-xs full-width"
    :class="classCard"
    :style="`background-color: ${colorBackground}; color: ${colorText}`"
  >
    <div
      class="infoBox"
      :class="`text-${position}`"
    >{{ title }}</div>
    <div v-if="text" :class="classValue" v-html="text"></div>
    <div :class="classValue">{{ value }}</div>
  </q-card>
  <!-- BING -->
  <q-card flat bordered :class="classCard" v-if="type === 'bing'">
    <q-bar dense class="itens-center bg-transparent">
      <q-icon v-if="icon" dense :name="icon" style="font-size: 10px; margin-right: 6px;" />
      <div class="marquee full-width q-pr-sm"><span>{{ title }}</span></div>
    </q-bar>
    <q-card-section class="q-pa-none">
      <div class="q-ma-xs" style="font-size: 0.9em">{{ value }}</div>
      <div class="q-ma-xs" style="font-size: 0.9em">{{ text }}</div>
    </q-card-section>
  </q-card>
  <!-- PLACA CA -->
  <q-card bordered flat class="q-pa-none" v-if="type === 'carplate'">
    <div class="bg-primary text-center text-white" style="font-size: 0.7em">{{ title }}</div>
    <div class="q-ma-xs text-h4" :class="`text-${position}`">{{ value }}</div>
  </q-card>
  <!-- PLACA 2 CA -->
  <q-card bordered flat class="q-pa-none" v-if="type === 'carplate2'">
    <div class="bg-primary text-center text-white" style="font-size: 0.7em">{{ title }}</div>
    <div class="q-ma-xs" style="font-size: 0.9em">{{ value }}</div>
    <div class="q-ma-xs" style="font-size: 0.9em">{{ text }}</div>
  </q-card>
  <!-- PLACA 3 CA -->
  <q-card bordered flat class="q-pa-none" v-if="type === 'carplate3'">
    <div class="bg-primary text-center text-white" style="font-size: 0.7em">{{ title }}</div>
    <q-item :style="`background-color: ${colorBackground}`" class="q-pa-none">
        <q-item-section v-if="icon !== '' && position === 'left'" side :style="`background-color: ${colorBackground2}`"
                        class=" q-pa-lg q-mr-none text-white">
          <q-icon :name="icon" color="white" size="24px"></q-icon>
        </q-item-section>
        <q-item-section class=" q-pa-md q-ml-none text-white">
          <q-item-label class="text-white text-subtitle text-weight-bolder">{{ value }}</q-item-label>
          <q-item-label>{{ text }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="icon !== '' && position === 'right'" :style="`max-width: 66px; background-color: ${colorBackground2}`"
                        class=" q-pa-lg q-mr-none text-white">
          <q-icon :name="icon" color="white" size="24px"></q-icon>
        </q-item-section>
      </q-item>
  </q-card>
</template>

<script>
import { QCard } from 'quasar'

export default {
  name: 'CptCards',
  extends: QCard,
  props: {
    position: {
      type: String,
      required: false,
      default: 'left'
    },
    type: {
      type: String,
      default: 'basic'
    },
    cardclass: {
      type: String,
      default: 'bg-transparent no-border no-shadow'
    },
    title: {
      type: String,
      default: ''
    },
    avatar: {
      type: String,
      default: ''
    },
    imgbackground: {
      type: String,
      default: ''
    },
    text: {
      type: String,
      default: ''
    },
    icon: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    colorBackground: {
      type: String,
      default: ''
    },
    colorBackground2: {
      type: String,
      default: ''
    },
    colorText: {
      type: String,
      default: ''
    },
    id: {
      type: String,
      default: ''
    },
    classValue: {
      type: String,
      default: 'subtitulo text-center text-bold'
    },
    classCard: {
      type: String,
      default: ''
    },
    classBar: {
      type: String,
      default: ''
    },
    bordered: {
      type: [Boolean],
      default: () => false
    },
    dds: { type: [Object, Array] }
  },
  setup () {
    return {}
  }
}
</script>

<style lang="sass" scoped>
.bing-card
  width: 80px
  height: 80px
</style>

<style scoped>
.marquee {
  width: 100px;
  height: 22px;
  overflow: hidden;
  white-space: nowrap;
}
.marquee span {
  font-size: 10px;
  display: inline-block;
  padding-left: 100%;
  animation: marquee 8s linear infinite;
}
@keyframes marquee {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(-100%, 0);
  }
}
</style>

<style lang="scss">
.infoBox {
  font-size: 10px;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
}
.infoBox1 {
  background-color: $red-4;
  color: white;
}
.infoBox2 {
  background-color: $orange-4;
  color: white;
}
.infoBox3 {
  background-color: $blue-4;
  color: white;
}
.infoBox4 {
  background-color: $grey-5;
  color: white;
}
.infoBox5 {
  background-color: $teal-4;
  color: white;
}
.infoBox6 {
  background-color: $green-4;
  color: white;
}
</style>

<style scoped>
@import 'src/css/adminlte/cores.css';
@import 'src/css/adminlte/infobox.css';
</style>
