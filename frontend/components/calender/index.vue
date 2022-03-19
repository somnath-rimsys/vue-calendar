<template>
  <div class="w-full">
    <table class="m-auto w-full text-white table">
      <thead>
        <tr class="h-16 flex justify-between items-center bg-indigo-600">
          <td class="ml-4"><h1 class="text-2xl">{{ month }},{{ year }}</h1></td>
          <td class="mr-4 text-right">
            <form-select :values="months" />
            <form-input
              class="w-1/6"
              type="text"
              :value="year"
              placeholder="Year"
            />
            <form-button
              :type="'button'"
              :theme="'error'"
              @onClick="btnClick"
            >
              Search
            </form-button>
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
      <tbody>
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
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api'
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
    let currentMonth = ref(props.month)
    const weeks = ref(Weeks)
    const months = ref(Months)
    let monthDays = ref([
      ['','',1,2,3,4,5],
      [6,7,8,9,10,11,12],
      [13,14,15,16,17,18,19],
      [20,21,22,23,24,25,26],
      [27,28,29,30,31,'','']
    ]);

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

    function btnClick() {
      console.log('Button clicked')
    }

    return {
      // data
      currentMonth,
      weeks,
      monthDays,
      months,

      //methods
      getBorder,
      getWeekInitial,
      btnClick,
    }
  },
})
</script>
