<template>
  <main>
    <div class="m-auto w-10/12">
      <calender
        :year = selectedYear
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
    let selectedYear = ref(new Date().getFullYear())

    return {
      //data
      selectedMonth,
      selectedYear,
    }
  },
})
</script>
