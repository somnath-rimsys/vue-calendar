<template>
  <div class="w-full">
    <table class="m-auto w-full text-white">
      <thead>
        <tr class="h-20 flex bg-gray-800">
          <td
            v-for="(week, key, index) in weeks"
            :key="key"
            class="w-full h-full flex justify-center items-center"
            :class="getBorder(index, 'thead')"
          >
            {{getWeekInitial(week)}}
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
              column ? 'bg-gray-600 cursor-pointer': 'bg-gray-500'
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
    month: {
      required: true,
      default: Months.JAN
    }
  },

  setup(props) {
    let currentMonth = ref(props.month)
    const weeks = ref(Weeks)
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

    return {
      // data
      currentMonth,
      weeks,
      monthDays,

      //methods
      getBorder,
      getWeekInitial,
    }
  },
})
</script>
