<template>
  <div>
    <el-button @click="logout" type="danger" class="logout" >退出</el-button>
  </div>
</template>
<script>
  export default {
    // 声明周期函数
    beforeCreate() {
    },
    methods: {
      logout() {
        window.sessionStorage.removeItem("token");
        // 编程式导航
        this.$router.push("login");
      },
    }
  };
</script>
<style>
  .el-menu {
    border-right: none;
  }
  .logout {
    float:right;
  }
</style>
