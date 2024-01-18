<template>
  <div class="login-container">
<div class="left">

</div>
<div class="right">
  <h1>手机号登录</h1>
  <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
  <el-form-item prop="username">
    <el-input v-model="ruleForm.username" placeholder="请输入用户名"></el-input>
  </el-form-item>
  <el-form-item prop="password">
    <el-input v-model="ruleForm.password"  placeholder="请输入密码"></el-input>
  </el-form-item>
  <el-form-item>
            <el-checkbox v-model="ruleForm.isAgree">用户平台使用协议</el-checkbox>
          </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
  </el-form-item>
</el-form>
</div>
  </div>
</template>

<script>
import { validUsername } from '@/utils/validate'

export default {
    data() {
      return {
        ruleForm: {
username:"",
password:"",
isAgree:false
        },
        rules: {
          username: [
            { required: true, message: '请输入手机号', trigger: 'blur' },
          {
            pattern:/^1[3-9]\d{9}$/,
            message: '手机号格式不正确', trigger: 'blur'
          }
          ],
          password:[
            { required: true, message: '请输入密码', trigger: 'blur' },
            { min: 1, max: 6, message: '长度在 1 到 6 个字符', trigger: 'blur' }
          ],
isAgree:[
  {validator:(rule,value,callback)=>{
    // rule:当前规则
    // value:当前绑定的值
    // callback:必须执行的函数
    value ? callback() : callback(new Error('请同意用户平台使用协议'))
  }}
]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
    }
  }
</script>

<style lang="scss" scoped>
.login-container {
  width: 100vw;
  height: 100vh;
  display: flex;
  .left{
    height: 100vh;
    flex: 3;
    background: url("../../assets/common/login_back.png");
    background-size: 100%;
  }
}
.right{
  padding: 10% 0;
  height: 100vh;
  flex: 2;
  box-sizing: border-box;
  h1{
    margin-left: 100px;
  }
}
</style>
