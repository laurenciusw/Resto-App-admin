<template>
  <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
    <div class="my-2 flex sm:flex-row flex-col justify-end">
      <button
        @click.prevent="changeSection('cuisineForm')"
        class="text-sm bg-gray-300 hover:bg-gray-400 text-gray-800 font-semibold py-2 px-4 rounded-full"
      >
        Add New Cuisine
      </button>
    </div>
    <div class="inline-block min-w-full shadow rounded-lg overflow-hidden">
      <table class="min-w-full leading-normal">
        <thead>
          <tr>
            <th
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Cusinename
            </th>
            <th
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Image
            </th>
            <th
              class="px-6 py-5border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Description
            </th>

            <th
              class="px-6 py-5border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Author
            </th>
            <th
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Price
            </th>
            <th
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Status
            </th>
            <th
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              Action
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="el in cuisine" :key="el.id">
            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <p class="text-gray-900 whitespace-no-wrap">{{ el.name }}</p>
            </td>
            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <div class="flex items-center">
                <div class="flex-shrink-0 w-30 h-30">
                  <img class="w-full h-20" :src="el.imgUrl" alt="" />
                </div>
                <div class="ml-3">
                  <p class="text-gray-900 whitespace-no-wrap"></p>
                </div>
              </div>
            </td>
            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <p class="text-gray-900 whitespace-no-wrap">{{ el.description }}</p>
            </td>

            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <p class="text-gray-900 whitespace-no-wrap">{{ el.User.email }}</p>
            </td>

            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <p class="text-gray-900 whitespace-no-wrap">Rp {{ el.price }}</p>
            </td>

            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <span>
                <div class="relative">
                  <select
                    class="appearance-none h-full rounded-l border block appearance-none w-full bg-white border-gray-400 text-gray-700 py-2 px-4 pr-8 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                  >
                    <option>Active</option>
                    <option>Inactive</option>
                    <option>archive</option>
                  </select>
                  <div
                    class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
                  >
                    <svg
                      class="fill-current h-4 w-4"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                    >
                      <path
                        d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                      />
                    </svg>
                  </div>
                </div>
              </span>
            </td>

            <td class="px-5 py-5 border-b border-gray-200 bg-white text-sm">
              <a href="#" class="flex items-center hover:text-blue-600">
                <span class="text-2xl"><i class="bx bx-edit-alt"></i></span>
              </a>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: ['cuisine'],
  name: 'cuisineTable',
  methods: {
    changeSection(destination) {
      this.$emit('changeSection', destination)
    }
  }
}
</script>

<style></style>
