<script setup>
import HeaderMenu from './components/header-menu/HeaderMenu.vue';
import ContentList from './components/content-list/ContentList.vue';
</script>

<template>
  <div class="container">
    <HeaderMenu />
    <!-- <HelloWorld msg="You did it!" /> -->

    <ContentList />
  </div>
</template>

<style scoped>
.menu-header {
  background-color: gray;
  width: 100%;
  height: 100px;
}
</style>
