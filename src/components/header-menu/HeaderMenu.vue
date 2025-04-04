<template>
  <div class="header-menu">
    <div class="top-left">
      <h1>TODO LIST</h1>
    </div>
    <div class="top-right">
      <img class="avatar-contact" src="https://www.w3schools.com/howto/img_avatar.png" alt="">
    </div>
  </div>
</template>
<script setup></script>
<style lang="scss" scoped>
.header-menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  .top-right {
    .avatar-contact {
      width: 50px;
      border-radius: 50%;
      cursor: pointer;
    }
  }
}
</style>