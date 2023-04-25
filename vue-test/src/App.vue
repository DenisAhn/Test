<template>
  <div class="container">
    <div class="table-container">
      <Table :items="items" :deleteItem="deleteItem" />
    </div>
    <button @click="showModal">Добавить</button>
    <Modal
      :items="items"
      :isActive="isModalActive"
      :closeModal="closeModal"
      :addItem="addItem"
    />
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
import Table from "./components//Table/Table.vue";
import Modal from "./components//Modal/Modal.vue";

export default {
  components: {
    Table,
    Modal,
  },
  setup() {
    const items = ref(
      JSON.parse(localStorage.getItem("users") || "[]")
    );
    const isModalActive = ref(false);
    const showModal = () => {
      isModalActive.value = true;
    };

    const closeModal = () => {
      isModalActive.value = false;
    };

    const addItem = (item) => {
      items.value.push(item);
    };

    const deleteItem = (index) => {
      items.value.splice(index, 1);
    };
    watchEffect(() => {
      localStorage.setItem("users", JSON.stringify(items.value));
    });

    return {
      items,
      isModalActive,
      showModal,
      closeModal,
      addItem,
      deleteItem,
    };
  },
};
</script>

<style
  src = "./App.css">
</style>
