<template>
  <div class="flex flex-col">
    <div class="-my-2 overflow-x-auto sm:overflow-hidden sm:-mx-3 lg:-mx-5">
      <div class="py-2 align-middle inline-block min-w-full sm:px-8 lg:px-9">
        <div>
          <span class="text-gray-700 block px-5 py-5 text-base font-medium">
            Employees
          </span>
        </div>
        <div
          class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
        >
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Employee
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Last Login
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Department
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Status
                </th>
              </tr>
            </thead>
            <tbody
              v-for="elem in data"
              :key="elem.id"
              class="bg-white divide-y divide-gray-200"
            >
              <tr>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-0 h-10 w-10">
                      <img
                        class="h-10 w-10 rounded-full"
                        :src="elem.profile_img"
                        alt=""
                      />
                    </div>
                    <div class="ml-4">
                      <div class="text-sm font-medium text-gray-900">
                        {{ elem.first_name }} {{ elem.last_name }}
                      </div>
                      <div class="text-sm text-gray-500">
                        {{ elem.email }}
                      </div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900">
                    {{ formatDate(elem.sessions[0]) }}
                  </div>
                  <div class="text-sm text-gray-500">
                    {{ formatDateRelative(elem.sessions[0]) }}
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {{ elem.department }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span
                  v-if="elem.status === true"
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full text-green-400"
                  >
                    Active
                  </span>
                  <span
                    v-else
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full text-red-500"
                  >
                    False
                  </span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "DataTable",
  props: ["data"],
  methods: {
    formatDateRelative: (date) => {
      return moment(date).startOf("day").fromNow();
    },
    formatDate: (date) => {
      return moment(date).format("MMMM D, YYYY");
    },
  },
};
</script>

<style>
</style>