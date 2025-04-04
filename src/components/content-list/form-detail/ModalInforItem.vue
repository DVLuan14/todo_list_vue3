<template>
	<div class="form-create">
		<div v-if="visibleModal" class="modal">
			<h3>Detail Item</h3>
			<form @submit.prevent="editItemDetail">
					<div class="form-group">
						<label>Title:</label>
						<input disabled v-model="formData.title" required />
					</div>
					<div class="form-group">
						<label>Content:</label>
						<input disabled v-model="formData.content" type="text" required />
					</div>
					<div class="form-group">
					</div>
					<button type="submit" @click="handleEditItem(formData)" class="submit-btn">Edit</button>
					<button type="button" @click="handleCancel()" class="cancel-btn">Cancel</button>
			</form>
		</div>
	</div>
</template>
<script setup>
import { reactive, watch } from 'vue';
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
const emit = defineEmits(['closeModal', 'switchEditFromDetail']);
const formData = reactive(
  {
    title: props.dataProp?.title || '',
    content: props.dataProp?.content ||'',
  }
);
watch(
  () => props.dataProp,
  (newProduct) => {
    if (newProduct) {
      formData.title = newProduct.title;
      formData.content = newProduct.content;
    }
  },
  { deep: true }
);

const handleCancel = () => {
	emit('closeModal');
}
const handleEditItem = (data) => {
	console.log('data', data);
}
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