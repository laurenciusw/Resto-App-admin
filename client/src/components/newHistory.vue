<template>
  <mytable :columns="columns" :data="histories" />
</template>

<script>
import mytable from './mytable.vue'

export default {
  name: 'newHistory',
  components: {
    mytable
  },
  props: ['histories'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'id' },
        { label: 'nama', field: 'name' },
        { label: 'descriptopn', field: 'description' },
        { label: 'updatedBy', field: 'updatedBy' },
        { label: 'createdAt', field: 'createdAt' }
      ]
    }
  }
}
</script>

<style></style>
