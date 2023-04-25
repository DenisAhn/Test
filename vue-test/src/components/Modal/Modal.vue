<template>
  <div class="modal" :class="{ active: isActive }">
    <div class="modal-content">
      <h2>Добавить</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="phone">Телефон:</label>
          <input
            type="text"
            id="phone"
            v-model="phone"
            :class="{ 'is-invalid': phoneError }"
            @blur="validatePhone"
          />
          <div class="invalid-feedback" v-if="phoneError">
            Please enter a valid phone number
          </div>
        </div>
        <div class="form-group">
          <label for="name">Имя:</label>
          <input
            type="text"
            id="name"
            v-model="name"
            :class="{ 'is-invalid': nameError }"
            @blur="validateName"
          />
          <div class="invalid-feedback" v-if="nameError">
            Please enter a name
          </div>
        </div>
        <div class="form-group">
          <label for="parent">Начальник:</label>
          <select id="parent" v-model="parent">
            <option value="">None</option>
            <option v-for="(item, index) in items" :value="item.name" :key="index">
              {{ item.name }}
            </option>
          </select>
        </div>
        <div class="form-actions">
          <button type="submit">Save</button>
          <button type="button" @click="closeModal">Cancel</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    items: {
      type: Array,
      default: () => [],
    },
    isActive: {
      type: Boolean,
      default: false,
    },
    closeModal: {
      type: Function,
      required: true,
    },
    addItem: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const phone = ref(null);
    const name = ref(null);
    const parent = ref(null);

    const phoneError = ref(false);
    const nameError = ref(false);

    const validatePhone = () => {
      if (!phone.value) {
        phoneError.value = true;
      } else {
        const phoneRegex = /^[+]*[(]{0,1}[0-9]{1,4}[)]{0,1}[-\s\./0-9]*$/;
        phoneError.value = !phoneRegex.test(phone.value);
      }
    };

    const validateName = () => {
      nameError.value = !name.value;
    };

    const handleSubmit = () => {
      validatePhone();
      validateName();

      if (!phoneError.value && !nameError.value) {
        props.addItem({
          phone: phone.value,
          name: name.value,
          parent: parent.value || null,
        });
        phone.value = null;
        name.value = null;
        parent.value = null;
        props.closeModal();
      }
    };

    return {
      phone,
      name,
      parent,
      phoneError,
      nameError,
      validatePhone,
      validateName,
      handleSubmit,
    };
  },
};
</script>

<style
  src ="./Modal.css">
</style>
