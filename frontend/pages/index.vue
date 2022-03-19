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
