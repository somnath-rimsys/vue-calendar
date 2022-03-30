<template>
  <button
    class="pl-2 pr-2 w-auto h-8"
    :class="btnTheme"
    @click="clicked"
  >
    <slot />
  </button>
</template>

<script>
import { defineComponent, onMounted, ref } from '@vue/composition-api'

export default defineComponent({
  props: {
    theme: {
      type: String,
      required: false,
      default: 'primary'
    }
  },
  setup(props, { emit }) {
    let btnTheme = ref();

    onMounted(()=>{
      if(props.theme === 'primary') {
        btnTheme.value = 'shadow bg-blue-800'
      }
      else if(props.theme === 'secondary') {
        btnTheme.value = 'shadow bg-gray-800'
      }
      else if(props.theme === 'success') {
        btnTheme.value = 'shadow bg-green-800'
      }
      else if(props.theme === 'error') {
        btnTheme.value = 'shadow bg-red-800'
      }
    })

    /**
     * Emmits custom event.
     */
    function clicked() {
      emit('onClick')
    }

    return {
      //data
      btnTheme,

      //methods
      clicked,
    }
  },
})
</script>
