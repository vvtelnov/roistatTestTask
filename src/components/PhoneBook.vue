<template>
  <div class="phonebook">
    <TableRow
      firstCol="Имя"
      secondCol="Телефон"
      :hasNestedRows="false"
    />
    <div v-if="phoneBookRows.length === 0">
      <p class="phonebook__empty-text">Телефонная книга пока пуста.</p>
    </div>
    <div v-else>
      <TableBody :tableRows="phoneBookRows" />
    </div>
  </div>
</template>

<script>
import TableBody from './TableBody.vue';
import TableRow from './TableRow.vue';

export default {
  name: "PhoneBook",
  components: { TableBody, TableRow },
  props: {
    phoneBookRows: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style scoped>
  .phonebook {
    width: 100%;
  }

  .phonebook__empty-text {
    padding: 20px 0;
    border: 1px solid teal;
    text-align: center;
    font-size: 16px;
    line-height: 1.5;
  }

  @media screen and (max-width: 820px) {
    .phonebook__empty-text {
      font-size: 18px;
      line-height: 1.6;
    }
  }
</style>
