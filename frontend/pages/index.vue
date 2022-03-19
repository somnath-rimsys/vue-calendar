<template>
  <main>
    <div class="m-auto w-11/12">
      <calender
        :month = selectedMonth
      />
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api'
import { Months } from '@/lib/constants'

export default defineComponent({
  name: 'HomePage',
  setup() {
    let selectedMonth = ref(Months.MAR)

    return {
      selectedMonth,
    }
  },
})
</script>
