<template>
  <select class="text-black outline-none w-auto h-8 bg-white">
    <option
      v-for="(data, index) in values"
      :key="index"
      :value="data"
      :selected="data === selected ? true : false"
      class="pt-1 pb-1 bg-white h-8"
    >
      {{data}}
    </option>
  </select>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  props: {
    values: {
      required: true,
    },
    selected: {
      required: false,
    }
  },
  setup() {

  },
})
</script>
