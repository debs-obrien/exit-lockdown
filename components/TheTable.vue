<template>
  <div class="flex flex-col">
    <div class="-my-2 py-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
      <div
        class="align-middle inline-block min-w-full shadow overflow-hidden sm:rounded-lg border-b border-gray-200"
      >
        <table class="min-w-full">
          <thead>
            <tr>
              <th
                v-for="(heading, index) in tableHeadings"
                :key="index"
                class="px-6 py-3 border-b border-gray-200 bg-gray-50 text-center text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider"
              >
                {{ heading }}
              </th>
            </tr>
          </thead>
          <tbody class="bg-white">
            <tr v-for="(item, index) in food" :key="index">
              <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
                <div class="flex items-center">
                  <div class="flex-shrink-0 h-auto w-24">
                    <img class="h-auto w-24" :src="item.img" :alt="item.name" />
                  </div>
                  <div class="ml-4">
                    <div class="text-sm leading-5 font-medium text-gray-900">
                      {{ item.name }}
                    </div>
                  </div>
                </div>
              </td>
              <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
                <div class="text-sm leading-5 text-gray-500">
                  {{ item.where }}
                </div>
              </td>
              <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
                <span
                  class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800"
                >
                  {{ item.status }}
                </span>
              </td>
              <td
                class="px-6 py-4 whitespace-no-wrap border-b border-gray-200 text-sm leading-5 text-gray-500"
              >
                {{ item.priority }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
import gql from 'graphql-tag'
export const food = gql`
  query {
    food {
      id
      img
      name
      priority
      status
      where
    }
  }
`
export default {
  data() {
    return {
      tableHeadings: ['What I miss', 'Place', 'Status', 'Priority'],
      food: []
    }
  },
  apollo: {
    $loadingKey: 'loading',
    food: {
      query: food
    }
  }
}
</script>
