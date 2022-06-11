<template>
  <div class="login-container">
    <el-form :model="form" class="login-form" :rules="rules" ref="formRef">
      <div class="title-container">
        <h3 class="title">用户登录</h3>
      </div>

      <el-form-item prop="username">
        <el-icon :size="20" class="svg-container">
          <Avatar />
        </el-icon>
        <el-input
          v-model="form.name"
          placeholder="用户名"
          maxlength="30"
          show-word-limit
        />
      </el-form-item>

      <el-form-item prop="password">
        <el-icon :size="20" class="svg-container">
          <Lock />
        </el-icon>
        <el-input
          v-model="form.password"
          placeholder="密码"
          maxlength="20"
          show-word-limit
        />
      </el-form-item>

      <el-button type="primary" class="login-button" @click="handleLogin"
        >登录</el-button
      >
    </el-form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const form = ref({
  name: '',
  password: ''
})

const CheckPassword = (rule, value, callback) => {
  let reg = /[0-9]/
  let flag = reg.test(value)
  if (flag === false) {
    callback(new Error('密码必须包含数字'))
  }

  reg = /[a-z]/
  flag = reg.test(value)
  if (flag === false) {
    callback(new Error('密码必须包含小写字母'))
  }

  reg = /[A-Z]/
  flag = reg.test(value)
  if (flag === false) {
    callback(new Error('密码必须包含大写字母'))
  }
  callback()
}

const rules = ref({
  username: [
    {
      min: 3,
      max: 30,
      message: '用户名要求3-30位！',
      trigger: 'blur'
    },
    {
      required: true,
      message: '请输入用户名！',
      trigger: 'blur'
    }
  ],
  password: [
    {
      required: true,
      message: '请输入密码！',
      trigger: 'blur'
    },
    {
      min: 8,
      max: 20,
      message: '密码要求8-20位！',
      trigger: 'blur'
    },
    {
      validator: CheckPassword,
      trigger: 'blur'
    }
  ]
})

const formRef = ref(null)
const handleLogin = () => {
  formRef.value.validate((valid) => {
    if (valid) {
      alert('submit！')
    } else {
      console.log('error submit!')
      return false
    }
  })
}
</script>

<style lang="scss" scoped>
$bg: #eeeeee;
$dark_gray: #888888;
$light_gray: #eee;
$cursor: #333333;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;

  .login-form {
    position: relative;
    width: 600px;
    max-width: 100%;
    overflow: hidden;
    margin: 120px auto;

    ::v-deep .el-form-item {
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 8px;
      width: 90%;
      margin: 50px 0px 0px 100px;
    }

    ::v-deep .el-input {
      display: inline-block;
      height: 40px;
      background: transparent;
      width: 90%;

      input {
        width: 100%;
        background: transparent;
        border: 0px;
        -webkit-appearance: none;
        border-radius: 0px;
        padding: 12px 10px 12px 10px;
        height: 40px;
        caret-color: $cursor;
        font-size: 20px;
      }
    }
    .login-button {
      width: 50%;
      box-sizing: border-box;
      margin: 100px 0px 0px 160px;
      font-size: 20px;
    }
  }

  .tips {
    font-size: 16px;
    line-height: 28px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: #333333;
      margin: 0px auto 60px auto;
      text-align: center;
      font-weight: bold;
    }

    ::v-deep .lang-select {
      position: absolute;
      top: 4px;
      right: 0;
      background-color: white;
      font-size: 22px;
      padding: 4px;
      border-radius: 4px;
      cursor: pointer;
    }
  }

  .show-pwd {
    // position: absolute;
    // right: 10px;
    // top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }
}
</style>
