<template>
  <div class="flex items-center justify-center p-12">
    <div class="mx-auto w-full max-w-[550px]">
      <form @submit.prevent="cuisineDetail ? updateCuisine() : addCuisine()">
        <div class="mb-5">
          <!-- name -->
          <label for="name" class="mb-3 block text-base font-medium text-[#07074D]">
            Cuisine Name
          </label>
          <input
            v-model="newCuisine.name"
            type="text"
            name="name"
            id="name"
            placeholder="Cuisine Name"
            class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          />
        </div>

        <!-- Description -->
        <div class="mb-5">
          <label for="description" class="mb-3 block text-base font-medium text-[#07074D]">
            Description
          </label>
          <textarea
            v-model="newCuisine.description"
            rows="4"
            name="description"
            id="description"
            placeholder="Cuisine Description"
            class="w-full resize-none rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          ></textarea>
        </div>

        <!-- price -->
        <div class="mb-5">
          <label for="email" class="mb-3 block text-base font-medium text-[#07074D]"> Price </label>
          <input
            v-model="newCuisine.price"
            type="number"
            name="price"
            id="price"
            placeholder="Cuisine Price"
            class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          />
        </div>

        <!-- imgUrl -->
        <div class="mb-5">
          <label for="imgUrl" class="mb-3 block text-base font-medium text-[#07074D]">
            Subject
          </label>
          <input
            v-model="newCuisine.imgUrl"
            type="text"
            name="imgUrl"
            id="imgUrl"
            placeholder="Enter your imgUrl"
            class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          />
        </div>

        <!-- category -->
        <div class="mb-5">
          <label for="categoryId" class="mb-3 block text-base font-medium text-[#07074D]">
            Subject
          </label>
          <select id="categoryId" class="form-select" required v-model="newCuisine.categoryId">
            <option value="" selected disabled>-- Select Category --</option>
            <option value="1">Snacks</option>
            <option value="2">Non Vegetarian Foods</option>
          </select>
        </div>

        <div>
          <button
            type="sumbit"
            class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-base font-semibold text-white outline-none"
          >
            Submit
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newCuisine: {
        name: '',
        description: '',
        price: '',
        imgUrl: '',
        categoryId: ''
      }
    }
  },

  methods: {
    addCuisine() {
      this.$emit('handleAddCuisine', this.newCuisine)
    },
    updateCuisine() {
      this.$emit('editCuisine', this.newCuisine, this.cuisineDetail.id)
    }
  },
  name: 'cuisineForm',
  props: ['cuisineDetail'],
  created() {
    if (this.cuisineDetail) {
      console.log(this.cuisineDetail, 'dari form')
      ;(this.newCuisine.name = this.cuisineDetail.name),
        (this.newCuisine.description = this.cuisineDetail.description),
        (this.newCuisine.price = this.cuisineDetail.price),
        (this.newCuisine.imgUrl = this.cuisineDetail.imgUrl),
        (this.newCuisine.categoryId = this.cuisineDetail.categoryId)
    }
  }
}
</script>

<style></style>
