<template>
  <div class="main-container">
    <!-- 框架的最外层 -->
    <el-container>
      <!-- 框架的头部 -->
      <el-header>
        <el-row>
          <el-col :span="4">
            <div class="grid-content bg-purple">
              <img src="../assets/logo.png" alt="">
            </div>
          </el-col>
          <el-col :span="18">
            <div class="grid-content bg-purple-light">
              电商后台管理系统
            </div>
          </el-col>
          <el-col :span="2">
            <div class="grid-content bg-purple">
              <el-button @click="logout" type="danger" class="logout">退出</el-button>
            </div>
          </el-col>
        </el-row>
      </el-header>
      <!-- 框架的下面左右两部分 -->
      <el-container>
        <!-- 框架的下面的左边部分 -->
        <el-aside width="200px">Aside</el-aside>
        <!-- 框架的下面的右边部分 -->
        <el-main>Main</el-main>
      </el-container>
    </el-container>
    <!-- 框架的最外层 -->
  </div>
</template>
<script>
  export default {
    // 声明周期函数
    beforeCreate() {},
    methods: {
      logout() {
        window.sessionStorage.removeItem("token");
        // 编程式导航
        this.$router.push("login");
      },
    }
  };
</script>
<style lang="scss">
  .main-container {
    //最外层的根元素大盒子
    height: 100%;
    //框架的部分
    .el-container {
      height: 100%;
      //框架的头部  
      .el-header,
      {
        background-color: #B3C0D1;
        color: #333;
        text-align: center;
        line-height: 60px;
        //框架内部的
         .el-col-18 {
          font-size: 30px;
          font-weight: 900;
          color: white;
        }
        .el-col-4 {
          text-align: center;
        }
        .el-col-2 {
          text-align: center;
        }
      }
      //下面的部分
     .el-container{

          .el-aside {
        background-color: #D3DCE6;
        color: #333;
        text-align: center;
        line-height: 200px;
      }
      .el-main {
        background-color: #E9EEF3;
        color: #333;
        text-align: center;
        line-height: 160px;
      }

     }
   
    }
  }
</style>
