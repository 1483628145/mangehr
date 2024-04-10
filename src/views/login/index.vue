<template>
  <div class="login-container">
    <div class="logo" />
    <div class="form">
      <h1>登录</h1>
      <el-card shadow="never" class="login-card">
        <!--登录表单-->
        <!--登录表单-->
        <!-- el-form > el-form-item > el-input -->
        <el-form ref="form" :model="form" :rules="rules">
          <el-form-item prop="mobile">
            <el-input v-model="form.mobile" placeholder="请输入手机号" />
          </el-form-item>
          <el-form-item prop="password">
            <el-input v-model="form.password" placeholder="请输入密码" show-password />
          </el-form-item>
          <el-form-item prop="isAgree">
            <el-checkbox v-model="form.isAgree">
              用户平台使用协议
            </el-checkbox>
          </el-form-item>
          <el-form-item>
            <el-button style="width:350px" type="primary" @click="login">登录</el-button>
          </el-form-item></el-form></el-card></div>
  </div></template>
<script>

export default {
  name: 'Login',
  data() {
    return {
      // 表单数据 13800000002 hm#qd@23!
      form: {
        mobile: '',
        password: '',
        isAgree: false
      },
      // 表单校验规则
      rules: {
        mobile: [
          // 必须输入并且验证格式是否正确 注意在设置pattern也就是正则的时候必须是 / /里面输入
          { required: true, message: '请输入手机号码', trigger: 'blur' },
          { pattern: /^1[3-9]\d{9}$/, message: '手机号格式不正确', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { pattern: /^.{6,12}$/, message: '密码的长度在6到12位', trigger: 'blur' }
        ],
        // 使用自定义规则校验是否勾选协议
        isAgree: [
          {
            validator: (rule, value, callback) => {
              /*
              第一个参数：代表规则
              第二个参数：代表校验的值
              第三个参数：代表回调函数 成功和失败都需要调用这个函数
              */
              if (value) {
                callback()
              } else {
                callback(new Error('请勾选使用协议'))
              }
            }
          }
        ]
      }
    }
  },
  methods: {
    // 登录按钮
    login() {
      console.log(this.$refs)
      this.$refs.form.validate((isOk) => {
        if (isOk) {
          console.log('success')
        }
      })
    }
  }
}
</script>
<style lang="scss">
.login-container {
  display: flex;
  align-items: stretch;
  height: 100vh;
  .logo {
    flex: 3;
    background: rgba(38, 72, 176) url(../../assets/common/login_back.png)
      no-repeat center / cover;
    border-top-right-radius: 60px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: center;
    padding: 0 100px;
    .icon {
      background: url(../../assets/common/logo.png) no-repeat 70px center /
        contain;
      width: 300px;
      height: 50px;
      margin-bottom: 50px;
    }
    p {
      color: #fff;
      font-size: 18px;
      margin-top: 20px;
      width: 300px;
      text-align: center;
    }
  }
  .form {
    flex: 2;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-left: 176px;
    .el-card {
      border: none;
      padding: 0;
    }
    h1 {
      padding-left: 20px;
      font-size: 24px;
    }
    .el-input {
      width: 350px;
      height: 44px;
      .el-input__inner {
        background: #f4f5fb;
      }
    }
    .el-checkbox {
      color:#606266;
    }
  }
}
</style>
