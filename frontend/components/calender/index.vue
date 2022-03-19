<template>
  <div class="w-full">
    <table class="m-auto w-full text-white table">
      <thead>
        <tr class="h-16 flex justify-between items-center bg-indigo-600">
          <td class="ml-4"><h1 class="text-2xl">{{ selectedMonth }},{{ selectedYear }}</h1></td>
          <td class="mr-4 text-right">
            <form-select
              :values="months"
              :selected="selectedMonth"
              @change="monthChange"
            />
            <form-input
              class="w-1/6"
              type="number"
              :value="year"
              placeholder="Year"
              @change="yearChange"
            />
          </td>
        </tr>
        <tr class="h-20 flex bg-gray-800">
          <td
            v-for="(day, key, index) in weeks"
            :key="key"
            class="w-full h-full flex justify-center items-center"
            :class="getBorder(index, 'thead')"
          >
            {{getWeekInitial(day)}}
          </td>
        </tr>
      </thead>
      <tbody v-if="monthDays">
        <tr
          v-for="(row, key) in monthDays"
          :key="'row'+key"
          class="h-20 flex"
        >
          <td
            v-for="(column, key) in row"
            :key="row+'-column-'+column+'-'+key"
            class="w-full h-full flex justify-center items-center border-t"
            :class="[
              getBorder({column, key}, 'tbody'),
              column
                ?'bg-gray-600 cursor-pointer hover:bg-gray-50 hover:text-black transition'
                : 'bg-gray-500'
            ]"
          >
            {{ column }}
          </td>
        </tr>
      </tbody>
      <tbody v-else>
        <tr><td class="text-black">Loading...</td></tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from '@nuxtjs/composition-api'
import { Months, Weeks } from '@/lib/constants'

export default defineComponent({
  name: 'CalenderHomePage',
  props: {
    year: {
      type: Number,
      required: true,
      default: new Date().getFullYear()
    },
    month: {
      type: String,
      required: true,
      default: Months.JAN
    }
  },

  setup(props) {
    let selectedMonth = ref(props.month)
    let selectedYear = ref(props.year)
    const weeks = ref(Weeks)
    const months = ref(Months)
    let monthDays = ref();

    onMounted(()=>{
      get()
    })

    /**
     * Get the month days array.
     */
    function get(): void {
      const date: Date = new Date(`${selectedMonth.value}-${selectedYear.value}`)
      const y: number = date.getFullYear()
      const m: number = date.getMonth();
      const firstDateOfMonth: number = new Date(y, m, 1).getDate()
      const lastDateOfMonth: number = new Date(y, m + 1, 0).getDate()
      const firstDateIndex: number = new Date(y, m, 1).getDay()
      let isinsertStart = false
      let tempMontsDays: Array<Array<number|string>> = []
      for(let i=0, x=firstDateOfMonth; i<5; i++) {
        let tempArr = []
        for(let j=0; j<7; j++) {
          if(firstDateIndex === j || isinsertStart) {
            if(x <= lastDateOfMonth) tempArr.push(x++)
            else tempArr.push('')
            isinsertStart = true
          }
          else tempArr.push('')
        }
        tempMontsDays.push(tempArr)
      }
      monthDays.value = tempMontsDays
    }

    /**
     * Function to remove border from the end td
     * @param index, tbody|thead
     * @returns string
     */
    function getBorder(index: number|any, type: 'thead'|'tbody'): string {
      if(type === 'thead') {
        return index != (Object.keys(weeks.value).length -1) ? 'border-r' : ''
      }
      else if(type === 'tbody') {
        if(index.key !== 6) return 'border-r'
        else return ''
      }
      else {
        return ''
      }
    }

    /**
     * Function to get the initial of each week string
     * @param week
     * @returns string
     */
    function getWeekInitial(week: Weeks): string {
      return week.split('')[0]
    }

    /**
     * Update the calender on month change
     */
    function monthChange(m: string): void {
      selectedMonth.value = m;
      get()
    }

    /**
     * Update the calender on year change
     */
    function yearChange(y: number): void {
      selectedYear.value = y;
      get()
    }

    return {
      // data
      weeks,
      months,
      selectedMonth,
      selectedYear,
      monthDays,

      //methods
      getBorder,
      getWeekInitial,
      monthChange,
      yearChange,
    }
  },
})
</script>
