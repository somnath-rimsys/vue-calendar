<template>
  <select class="text-black outline-none w-auto h-8 bg-white" @change="change($event)">
    <option
      v-for="(data, index) in values"
      :key="index"
      :value="index"
      :selected="data === selected ? true : false"
      class="pt-1 pb-1 bg-white h-8"
    >
      {{data}}
    </option>
  </select>
</template>

<script>
import { defineComponent , emit} from '@vue/composition-api'
import { Months } from '@/lib/constants'

export default defineComponent({
  props: {
    values: {
      required: true,
    },
    selected: {
      required: false,
    }
  },
  setup(_, {emit}) {
    /**
     * Emit custom event on change
     */
    function change(event) {
      const m = event.target.value
      emit('change', Months[m])
    }

    return {
      // methods
      change
    }
  },
})
</script>
