<template>
  <input
    class="text-black outline-none w-auto h-8 pl-1 pr-1"
    @change="change($event)"
  />
</template>

<script>
import { defineComponent, emit } from '@vue/composition-api'

export default defineComponent({
  setup(props, { emit }) {
    /**
     * Emit ustom event on hange
     */
    function change(event) {
      const y = Number(event.target.value)
      emit('change', y);
    }

    return {
      // methods
      change
    }
  },
})
</script>
