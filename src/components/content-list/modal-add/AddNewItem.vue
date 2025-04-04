<template>
  <div class="form-create">
    <div v-if="visibleModal" class="modal">
      <h3>{{ typeForm ? "Add New Item" : "Edit Item" }}</h3>
      <form @submit.prevent="submitForm">
          <div class="form-group">
            <label>Title:</label>
            <input v-model="formData.title" required />
          </div>
          <div class="form-group">
            <label>Content:</label>
            <input v-model="formData.content" type="text" required />
          </div>
          <div class="form-group">
          </div>
          <button type="submit" class="submit-btn">{{ typeForm ? "Add" : "Save" }}</button>
          <button type="button" @click="handleCancel()" class="cancel-btn">Cancel</button>
      </form>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref, watch } from 'vue';
const props = defineProps({
  visibleModal: {
    type: Boolean,
    default: false,
  },
  dataProp: {
    type: Object,
    required: true,
  }
});
const formData = reactive(
  {
    title: props.dataProp?.title || '',
    content: props.dataProp?.content ||'',
  }
);
const typeForm = ref(true);
watch(
  () => props.dataProp,
  (newProduct) => {
    if (newProduct) {
      typeForm.value = false;
      // formData.id = newProduct.id;
      formData.title = newProduct.title;
      formData.content = newProduct.content;
    } else {
      typeForm.value = true;
      resetForm();
    }
  },
  { deep: true }
);
const emit = defineEmits(['createItem', 'closeModal']);

const handleCancel = () => {
  emit('closeModal');
}
const submitForm = () => {
  console.log('formData', formData);
  emit('createItem', { ...formData });
  if (typeForm.value) {
    resetForm();
  }
}
const resetForm = () => {
  formData.title = '';
  formData.content = '';
};
</script>
<style lang="scss" scoped>
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 20px;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  z-index: 1000;
  width: 400px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.submit-btn {
  background-color: #28a745;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 48%;
  margin-right: 4%;
}

.cancel-btn {
  background-color: #dc3545;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 48%;
}

.submit-btn:hover { background-color: #218838; }
.cancel-btn:hover { background-color: #c82333; }
</style>