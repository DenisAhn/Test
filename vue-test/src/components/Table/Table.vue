<template>
  <table>
    <thead>
    <tr>
      <th>Phone</th>
      <th>Name</th>
      <th>Parent</th>
      <th>Action</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in items" :key="index">
      <td>{{ item.phone }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.parent || "-" }}</td>
      <td>
        <button class="delete-btn" @click="deleteItem(index)">Delete</button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    deleteItem: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style
  src ="./Table.css">
</style>
