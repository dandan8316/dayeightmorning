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
        <el-aside width="200px">
          <!-- 最外层的大菜单导航 -->
          <el-menu default-active="2" class="el-menu-vertical-demo" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b" router>
            <!-- 子菜单的部分 -->
            <el-submenu v-for="(item, index) in menuList" :key="item.id" :index="item.order+''">
              <!-- 顶部的导航一 -->
             <template slot="title">
                <i class="el-icon-location"></i>
                <span>{{item.authName}}</span>
              </template>
              <!-- 下面的子菜单导航组 -->
              <el-menu-item-group>
             <el-menu-item v-for="(it, i) in item.children" :key="it.id" :index="'/'+it.path" >
                <i class="el-icon-menu"></i>
                {{it.authName}}
              </el-menu-item>
              </el-menu-item-group>
            </el-submenu>

          </el-menu>
        </el-aside>
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
    // beforeCreate() {},
    data() {
      return {
    menuList: []

      }
    },
    methods: {
      logout() {
        this.$confirm('你真的要退出吗?', '提示', {
          confirmButtonText: '狠心退出',
          cancelButtonText: '再看看',
          type: 'warning'
        }).then(() => {
          window.sessionStorage.removeItem("token");
          // 编程式导航
          this.$router.push("login");
          //成功
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });
        });
      },
    }
    ,
    created() {
      this.$axios.get("menus", {

          // headers: {
          //   Authorization: window.sessionStorage.getItem("token")
          // }
        })
        .then(res => {
          this.menuList = res.data.data;
        })
    },
  };
</script>
<style lang="scss">
  .main-container {
    //最外层的根元素大盒子
    height: 100%; //框架的部分
    .el-container {
      height: 100%; //框架的头部  
      .el-header,
      {
        background-color: #B3C0D1;
        color: #333;
        text-align: center;
        line-height: 60px; //框架内部的
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
      } //下面的部分
      .el-container {
        .el-aside {
          background-color: #D3DCE6;
          color: #333;
          text-align: center;
          line-height: 200px;
          .el-submenu__title {
            text-align: left;
          }
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
