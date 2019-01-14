<template>
  <!-- 登录容器 -->
  <div class="login-container">
    <!-- 表单容器 -->
    <div class="form-container">
      <h2>用户登录</h2>
      <el-form label-position="top" :rules="rules" ref="formData" label-width="80px" :model="formData">
        <el-form-item label="用户名" prop="username">
          <el-input v-model="formData.username"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input type="password" v-model="formData.password"></el-input>
        </el-form-item>
        <el-button class="login-btn" type="primary" @click="submitForm('formData')">登录</el-button>
      </el-form>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        // 表单数据
        formData: {
          username: "",
          password: ""
        },
        // 表单验证规则
        rules: {
          username: [
            // required :必须
            // message: 提示信息
            // trigger: 触发时机
            // min:最短
            // max:最常
            {
              required: true,
              message: "请输入用户名",
              trigger: "change"
            },
            {
              min: 3,
              max: 10,
              message: "长度在 3 到 10 个字符",
              trigger: "change"
            }
          ],
          password: [{
              required: true,
              message: "请输入密码",
              trigger: "change"
            },
            {
              min: 6,
              message: "哥们,你密码太短了吧",
              trigger: "change"
            }
          ]
        }
      };
    },
    //方法
    methods: {
      submitForm(formName) {
        //$refs 数组 可以让我们通过 设定的名字 获取对应的的dom元素
        //通过表单元素的 validate(element-ui)增加的验证方法
        this.$refs[formName].validate((valid) => {
          if (valid) {
            // alert('submit!');
            //成功
            //调用axios调用接口
            // ---------------------------------------------------
            this.$axios.post("login", this.formData).then(res => {
              console.log(res);
              
              if (res.data.meta.status === 400) {
                //错误返回错误的信息
                this.$message.error(res.data.meta.msg);

              } else if (res.data.meta.status == 200) {
                //正确返回正确的信息
                this.$message.success(res.data.meta.msg);
                //正确了保存token sessionStorage
                window.sessionStorage.setItem("token",res.data.data.token);
                //然后去首页
                this.$router.push("/")

                // this.$message({
                //   message: res.data.meta.msg,
                //   type: "success"
                // });
              }
              
            });
            //-------------------------------------------

          } else {
            //失败了就提示
            //弹框提示
            this.$message.error("请正确输入用户名和密码")
            return false;
          }
        });
      },
    },
  }
</script>

<style lang="scss">
  .login-container {
    background-color: #324152;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .form-container {
      background-color: white;
      width: 580px;
      padding: 40px;
      box-sizing: border-box;
      border-radius: 10px;
      .login-btn {
        width: 100%;
      }
    }
  }
</style>
