<template>
  <q-table
    class="q-mt-md"
    title="Table Title"
    :rows="products"
    :columns="columns"
    row-key="name"
    no-data-label="no Products"
  />
</template>

<script>
// create a table for to show ours Datas
const columns = [
  {
    name: 'product',
    label: 'Product',
    align: 'left',
    field: 'product',
    sortable: 'true'
  },
  {
    name: 'prioridad',
    label: 'Prioridad',
    align: 'left',
    field: 'prioridad',
    sortable: 'true'
  }
]

export default {

  props: {
    products: Array
  },

  setup () {


    return { columns }
  }
}
</script>

<style lang="scss" scoped>

</style>
