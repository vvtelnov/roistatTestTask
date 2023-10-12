<template>
  <div class="table">
    <div
      v-for="(row, index) in tableRows"
      :key="index"
    >
      <TableRow
        :firstCol="row.name"
        :secondCol="row.phone"
        :hasNestedRows="hasNestedRows(row)"
        :marginForNestedLvl="calcMarginForNestedLvl"
      />
      <div v-if="hasNestedRows(row)">
        <TableBody :tableRows=row.nested :nestedLvl="nestedLvl + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import TableRow from './TableRow.vue';

export default {
  name: "TableBody",
  components: { TableRow },
  props: {
    tableRows: {
      type: Array,
      required: true,
    },
    nestedLvl: {
      type: Number,
      default: 0,
    }
  },
  methods: {
    hasNestedRows(row) {
      return Boolean(row.nested.length !== 0)
    }
  },
  computed: {
    calcMarginForNestedLvl() {
      return `${35 - this.nestedLvl * 5}%`
    }
  }

}
</script>

<style scoped>
  .table {
    width: 100%;
  }
</style>
