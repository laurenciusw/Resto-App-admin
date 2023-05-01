<template>
  <div>
    <mytable
      :columns="columns"
      :data="authorName"
      @detailCuisine="detailCuisine"
      @editStatus="editStatus"
    />
  </div>
</template>

<script>
import mytable from './mytable.vue'

export default {
  name: 'newCuisine',
  components: {
    mytable
  },
  props: ['cuisine'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'num' },
        { label: 'nama', field: 'name' },
        { label: 'image', field: 'imgUrl' },
        { label: 'description', field: 'description' },
        { label: 'author', field: 'author' },
        { label: 'price', field: 'price' },
        { label: 'status', field: 'status' },
        { label: 'action', field: 'action' }
      ]
    }
  },
  computed: {
    authorName() {
      return this.cuisine.map((el, index) => {
        el.num = index + 1
        el.price = el.price.toLocaleString('id-ID', {
          style: 'currency',
          currency: 'IDR'
        })
        el.author = el.User.email
        return el
      })
    }
  },
  methods: {
    detailCuisine(id) {
      console.log(id, 'id di cuisine')
      this.$emit('detailCuisine', id)
    },
    editStatus(id, newStatus) {
      this.$emit('editStatus', id, newStatus)
    }
  }
}
</script>

<style></style>
