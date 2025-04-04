<template>
  <div class="container">
    <div class="header-table">
      <button class="btn-primary" @click="addNew('add')">Add New</button>
    </div>
    <div class="table-todo">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Title</th>
            <th>Content</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in dataList" :key="item.id">
            <td>{{ item.id }}</td>
            <td style="cursor: pointer;" @click="viewDetail(item)">{{ item.title }}</td>
            <td>{{ item.content }}</td>
            <td class="form-action">
              <button @click="viewDetail(item)" class="action-btn detail">Detail</button>
              <button @click="editItem(item, 'edit')" class="action-btn edit">Edit</button>
              <button @click="deleteItem(item.id)" class="action-btn delete">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <AddNewItem :visibleModal="showModalAdd" :dataProp="selectedProduct" @createItem="handleCreate()" @closeModal="handleCloseModal()"></AddNewItem>
  <ModalInforItem :visibleModal="showModalDetail" :dataProp="selectedItem" @switchEditFromDetail="handleSwitchEdit()" @closeModal="handleCloseEdit()"></ModalInforItem>
</template>
<script setup>
import { reactive, ref } from 'vue';
import AddNewItem from './modal-add/AddNewItem.vue';
import ModalInforItem from './form-detail/ModalInforItem.vue';
const dataList = reactive([
  {
    id: 1,
    title: 'working something',
    content: 'test 123123'
  }, {
    id: 2,
    title: 'You have do it',
    content: 'test 123123'
  }, {
    id: 3,
    title: 'Cook lunch',
    content: 'test 123123'
  }
]);
const showModalAdd = ref(false);
const selectedProduct = ref(null);
const showModalDetail = ref(false);
const selectedItem = ref(null);
const addNew = () => {
  showModalAdd.value = true;
}
const editItem = (data, type) => {
  if (type === 'edit') {
    selectedProduct.value = data;
    showModalAdd.value = true;
  } else {
    selectedProduct.value = null;
    showModalAdd.value = true;
  }
}
const viewDetail = (data) => {
  selectedItem.value = data;
  showModalDetail.value = true;
}
const deleteItem = (id) => {
  if (confirm('Bạn có chắc muốn xóa sản phẩm này?')) {
    const index = dataList.findIndex(p => p.id === id);
    if (index !== -1) {
      dataList.splice(index, 1);
    }
  }
}
const handleCreate = (data) => {
  console.log('form submit', data); 
}
const handleSwitchEdit = (data) => {
  console.log('detail to edit', data); 
}
const handleCloseModal = () => {
  showModalAdd.value = false;
  selectedProduct.value = null;
}
const handleCloseEdit = () => {
  showModalDetail.value = false;
}

</script>
<style lang="scss" scoped>
.container {
  .header-table {
    .btn-primary {
      background-color: #0780ab;
      border: none;
      color: white;
      padding: 12px 30px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 4px 2px;
      cursor: pointer;
      border-radius: 5px;
      &:hover {
        background-color: #04698d;
      }
    }
  }
  .table-todo {
    background-color: gray;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    th, td {
      padding: 12px;
      text-align: left;
      border: 1px solid #ddd;
    }
    th {
      background-color: #007bff;
      color: white;
    }
    tr:nth-child(even) {
      background-color: #f2f2f2;
    }
    tr:hover {
      background-color: #ddd;
    }
    .form-action {
      width: 200px;
      text-align: center;
      .action-btn {
        cursor: pointer;
      }
      .edit {
        margin: 0 5px;
      }
    }
  }
}
</style>