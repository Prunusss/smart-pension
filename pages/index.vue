<template style="overflow-y: hidden">
  <div class="loginWrapper">
    <div class="back-ground" style="overflow-y: hidden; z-index: -1">
      <img src="../assets/image/index-background.jpg">
    </div>

    <el-tabs  class="bd" type="border-card">
      <el-tab-pane label="用户登录">
        <p class="title">
          欢迎使用智慧养老系统!
        </p>
        <el-form :model="loginForm" :rules="loginRule" ref="loginForm" :label-position="labelPosition">
          <el-form-item  prop="userName" class="login-item" style="margin: 0">
            <el-input type="userName" v-model="loginForm.userName" placeholder="账号" @keyup.enter.native="submitForm('loginForm')"></el-input>
          </el-form-item>
          <el-form-item prop="pwd" style="margin-top: 20px;margin-bottom: 0px">
            <el-input v-model="loginForm.pwd" placeholder="密码" type="password" @keyup.enter.native="submitForm('loginForm')"></el-input>
          </el-form-item>
          <el-form-item style="margin-top: 20px">
            <el-button type="primary" @click="submitForm('loginForm')" class="submitBtn" round >登录</el-button>
          </el-form-item>
        </el-form>
      </el-tab-pane>

    </el-tabs>

    <div style="position: absolute; height: 2rem; bottom: 2rem">

    </div>
  </div>
</template>

<script>
import login from '~/components/Login.vue'
import upload from '~/components/base/cliUpload.vue'
import axios from 'axios'
import Cookies from 'js-cookie';
import Pro from '../api/API_PRO'
import API from '../api'
import { getBrowser } from "../components/util";
import qs from 'qs'

export default {
  components: {

    login,upload
  },

  data () {
    return {
      loadingLogin: false,
      labelPosition: 'left',
      loginForm: {
        userName: '',
        pwd: ''
      },
      loginRule: {
        userName: [
          { required: true, message: '请输入用户名', trigger: 'blur' }
          //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
        ],
        pwd: [
          { required: true, message: '请输入密码', trigger: 'blur' }
          //{ min: 3, max: 20, message: '长度在 3 到 20 个字符', trigger: 'blur' }
        ]
      },
    }
  },

  mounted() {
      // 先登录
      this.misLogin();
  },
  methods: {
    submitForm (loginForm) {
      this.$refs[loginForm].validate((valid) => {
        if (!valid) {
          return
        }
        this.loadingLogin = true
      });
      axios.post('http://192.168.96.129:5050/api/login', qs.stringify({
        username: this.loginForm.userName,
        password: this.loginForm.pwd
      })).then(successResponse=>{
        if (successResponse.data.code === '200') {
          this.loadingLogin = false
          this.$router.push({path: `/main/admin`})
        } else if (successResponse.data.code === 201) {
          console.log(successResponse.data.code)
          this.loadingLogin = false
          alert('密码不正确！')
          return
        } else if (successResponse.data.code === '404') {
          console.log(successResponse.data.code)
          this.loadingLogin = false
          alert('用户名不存在！')
          return
        } else {
          console.log(successResponse.data.code)
          return
        }

      })

      // let type = Cookies.get('type');
      //
      // if (type === '0') {
      //   this.$router.push({path: `/main/admin`})
      // } else if (type === '1') {
      //   this.$router.push({path: `/main/user`})
      // }
    },
  }
}
</script>

<style scoped>
  .back-ground{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
  }
  .back-ground>img{
    width: 100%;
    height: 100%;
  }

  .bd{
    width: 20rem;
    margin-left: 8%;
    margin-top:15%;
    min-height: 15rem;
    background-color: #ffffff;
    border-radius: 5px;
  }
  .title{
    width: 100%;
    text-align: center;
    height: 2.5rem;
  }
  .title:after{
    display: inline-block;
    width: 100%;
    content: '';
  }

  /*
 按钮圆角
  */
  .submitBtn{
    display:block;
    margin:0 auto;
    border-radius: 25px;
    margin-bottom: 0px;
    font-size: 15px;
    background-color: #1965d9;
    transition: 1s;
    border-width: 0;
  }
</style>

