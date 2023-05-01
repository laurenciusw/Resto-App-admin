<template>
  <mytable :columns="columns" :data="categories" />
</template>

<script>
import mytable from './mytable.vue'

export default {
  name: 'newCategory',
  components: {
    mytable
  },
  props: ['categories'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'id' },
        { label: 'nama', field: 'name' }
      ]
    }
  }
}
</script>

<style></style>
