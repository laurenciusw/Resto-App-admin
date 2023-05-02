<template>
  <div>
    <main class="min-h-screen w-full bg-gray-100 text-gray-700" x-data="layout">
      <!-- header page -->
      <header
        class="flex w-full items-center justify-between border-b-2 border-gray-200 bg-white p-2"
      >
        <!-- logo -->
        <div class="flex items-center space-x-2">
          <button type="button" class="text-3xl" @click="asideOpen = !asideOpen">
            <i class="bx bx-menu"></i>
          </button>
          <div>Logo</div>
        </div>
        <div>
          <button
            type="button"
            @click="profileOpen = !profileOpen"
            class="h-9 w-9 overflow-hidden rounded-full"
          >
            <img src="https://plchldr.co/i/40x40?bg=111111" alt="plchldr.co" />
          </button>
        </div>
      </header>

      <div class="flex sticky top-0">
        <!-- aside -->
        <aside
          class="flex w-72 flex-col space-y-2 border-r-2 border-gray-200 bg-white p-2 sticky top-0"
          style="height: 90.5vh"
          :class="{ hidden: !asideOpen }"
        >
          <a
            @click.prevent="changeSection('')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600"
          >
            <span class="text-2xl"><i class="bx bx-home"></i></span>
            <span>home</span>
          </a>
          <a
            @click.prevent="changeSection('newCuisine')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-food-menu"></i></span>
            <span>Menu</span>
          </a>
          <a
            @click.prevent="changeSection('newCategory')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-category-alt"></i></span>
            <span>Category</span>
          </a>

          <a
            @click.prevent="changeSection('newHistory')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-history"></i></span>
            <span>History</span>
          </a>

          <br />
          <br />

          <hr />

          <a
            @click.prevent="doLogout"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-log-out"></i></span>
            <span>logout</span>
          </a>
        </aside>

        <!-- main content page -->
        <div class="container mx-auto px-4 sm:px-8">
          <div class="py-8">
            <!-- table -->

            <cuisineForm
              v-if="currentSection == 'cuisineForm'"
              @handleAddCuisine="handleAddCuisine"
              :cuisineDetail="cuisineDetail"
              @editCuisine="editCuisine"
            />

            <newHistory
              v-if="currentSection == 'newHistory'"
              @changeSection="changeSection"
              :histories="histories"
            />

            <newCategory
              v-if="currentSection == 'newCategory'"
              @changeSection="changeSection"
              :categories="categories"
            />

            <div v-if="currentSection == 'newCuisine'">
              <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
                <div class="my-2 flex sm:flex-row flex-col justify-end">
                  <button
                    @click.prevent="changeSection('cuisineForm')"
                    class="text-sm bg-gray-300 hover:bg-gray-400 text-gray-800 font-semibold py-2 px-4 rounded-full"
                  >
                    Add New Cuisine
                  </button>
                </div>
              </div>
              <newCuisine
                @changeSection="changeSection"
                :cuisine="cuisine"
                @detailCuisine="detailCuisine"
                @editStatus="editStatus"
              />
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import cuisineForm from './cuisineForm.vue'
import newHistory from './newHistory.vue'
import newCategory from './newCategory.vue'
import newCuisine from './newCuisine.vue'

export default {
  props: ['cuisine', 'categories', 'histories', 'cuisineDetail'],
  data() {
    return {
      asideOpen: true,
      currentSection: 'cuisineTable'
    }
  },
  components: {
    cuisineForm,
    newHistory,
    newCategory,
    newCuisine
  },
  methods: {
    changeSection(destination) {
      this.currentSection = destination
    },

    doLogout() {
      this.$emit('handleLogout')
    },

    doFetchCuisine() {
      this.$emit('handleFetchCuisine')
    },

    doFetchCategory() {
      this.$emit('handleFetchCategory')
    },
    doFetchHistory() {
      this.$emit('handleFetchHistory')
    },
    handleAddCuisine(newCuisine) {
      this.$emit('handleAddCuisine', newCuisine)
    },
    detailCuisine(id) {
      console.log(id, 'dihome')
      this.$emit('detailCuisine', id)
    },
    editCuisine(newCuisine, id) {
      this.$emit('editCuisine', newCuisine, id)
    },
    editStatus(id, newStatus) {
      this.$emit('editStatus', id, newStatus)
    }
  },
  created() {
    this.doFetchCuisine(), this.doFetchCategory(), this.doFetchHistory()
  }
}
</script>

<style></style>
