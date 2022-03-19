<template>
  <main class="h-screen bg-gray-200">
    <div class="m-auto pt-2 w-11/12">
      <app-card>
        <calendar
          :year = selectedYear
          :month = selectedMonth
        />
      </app-card>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api'
import { Months } from '@/lib/constants'

export default defineComponent({
  name: 'HomePage',
  setup() {
    const month = [
      Months.JAN,
      Months.FEB,
      Months.MAR,
      Months.APR,
      Months.MAY,
      Months.JUN,
      Months.JUL,
      Months.AUG,
      Months.SEP,
      Months.OCT,
      Months.NOV,
      Months.DEC
    ];
    let selectedMonth = ref(month[new Date().getMonth()])
    let selectedYear = ref(new Date().getFullYear())

    return {
      //data
      selectedMonth,
      selectedYear,
    }
  },
})
</script>
