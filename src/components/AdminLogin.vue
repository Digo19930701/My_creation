<template>
    <div class="login">
      <div class="title" style="font-size: 100px;">商家登入</div>
      <el-form :model="loginForm" class="loginForm" >
        <el-form-item label="帳號" :label-width="formLabelWidth">
          <el-input
            v-model="loginForm.account"
            autocomplete="off"
            style="height: 50px; width: 500px"
          />
        </el-form-item>
        <el-form-item label="密碼" :label-width="formLabelWidth">
          <el-input
            v-model="loginForm.password"
            autocomplete="off"
            style="height: 50px; width: 500px"
          />
        </el-form-item>
        <div style="margin-left: 130px">
          <el-button @click="response" style="width: 200px; height: 50px">登入</el-button>
          <el-button @click="dialogFormVisible = true" style="width: 200px; height: 50px"
            >註冊</el-button
          >
          <el-link @click="verifyEmail = true" style="color: red; margin-left: 20px"
            >忘記密碼</el-link
          >
        </div>
      </el-form>
  
      <div style="margin-top: 50px">
        <img src="./config/image/googleLogin.png" />
      </div>
  
      <el-dialog v-model="dialogFormVisible" title="註冊會員">
        <el-form :model="register">
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="register.mail"
              label-width="100px"
              autocomplete="off"
              type="register"
              placeholder="請輸入信箱"
              id="registerEamil"
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="register.Password"
              label-width="100px"
              autocomplete="off"
              type="register"
              placeholder="請輸入密碼"
              show-password
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="register.severid"
              label-width="100px"
              autocomplete="off"
              type="register"
              placeholder="請輸入統一編號"
              show-password
            />
          </el-form-item>
          <!-- <GoogleReCaptchaV2 style="margin-left: 60%" /> -->
          <label for="option1">
            <input type="checkbox" id="option1" name="option" /> 已閱讀註冊相關資訊 </label
          ><br />
        </el-form>
  
        <template #footer>
          <span class="dialog-footer">
            <el-button type="primary" @click="submitForm">註冊</el-button>
            <el-button @click="dialogFormVisible = false">取消</el-button>
          </span>
        </template>
      </el-dialog>
  
      <el-dialog v-model="verifyEmail" title="輸入信箱">
        <el-form :model="verifyemail">
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="verifyemail.mail"
              label-width="100px"
              autocomplete="off"
              type="forgetPs"
              placeholder="請輸入信箱"
            />
          </el-form-item>
        </el-form>
  
        <template #footer>
          <span class="dialog-footer">
            <el-button type="primary" @click="forgetPassword = true"> 下一步</el-button>
            <el-button @click="verifyEmail = false">取消</el-button>
          </span>
        </template>
      </el-dialog>
  
      <el-dialog v-model="forgetPassword" title="忘記密碼">
        <el-form :model="forgetPs">
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="forgetPs.verifypassword"
              label-width="100px"
              autocomplete="off"
              type="forgetPs"
              placeholder="請輸入驗證碼"
            />
          </el-form-item>
  
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="forgetPs.newpassword"
              label-width="100px"
              autocomplete="off"
              type="forgetPs"
              placeholder="輸入新密碼"
              show-password
            />
          </el-form-item>
        </el-form>
  
        <template #footer>
          <span class="dialog-footer">
            <el-button type="primary" @click="registerout"> 送出</el-button>
            <el-button @click="forgetPassword = false">取消</el-button>
          </span>
        </template>
      </el-dialog>
    </div>
  </template>
    
    <script lang="ts" setup>
  import { dataType } from 'element-plus/es/components/table-v2/src/common'
  import { reactive, ref } from 'vue'
  // import GoogleReCaptchaV2 from './GoogleReCaptchaV2.vue'
  import axios from 'axios'
  
  const dialogFormVisible = ref(false)
  const verifyEmail = ref(false)
  const forgetPassword = ref(false)
  const checkbox = ref(false)
  const formLabelWidth = '100px'
  
  const register = reactive({
    mail: '',
    Password: '',
    severid: ''
  })
  
  const forgetPs = reactive({
    verifypassword: '',
    newpassword: ''
  })
  const verifyemail = reactive({
    mail: ''
  })
  
  const loginForm = reactive({
    account: '',
    password: ''
  })
  
  const response = () => {
    const account = loginForm.account
    const password = loginForm.password
  
  //   console.log('account=' + account + '******' + 'password=' + password)
    console.log(`account=${account}`,`password=${password}`,1,2,3)
    // window.location.href = 'http://localhost:8080/api/login',{ account: account, password: password };
  
    const user = {
      acc: account,
      pass: password
    }
    axios
      .post('http://localhost:8080/SpringBoot/Login', user, {
        headers: {
           'Content-Type': 'application/x-www-form-urlencoded'
          }
      })
      .then((response) => {
          alert(response.data);
        console.log(response.data)
      })
      .catch((error) => {
          alert(error)
        console.error(error)
      })
  }
  
  const login = () => {
    console.log('loginForm', loginForm)
  }
  const registerout = () => {
    console.log('register', register)
  }
  
  function submitForm() {
    // console.log('in')
    var option1 = document.getElementById('option1')
  
    if (option1.checked) {
      alert('已勾選')
    } else {
      alert('請勾選註冊相關資訊')
    }
  
    // const ariaCheckedValue = checkboxElement.getAttribute('aria-checked');
    // console.log('aria-checked 属性的值:', ariaCheckedValue);
    // if (aria-checked == false) {
    //   const ariaCheckedValue = checkboxElement.getAttribute('aria-checked');
    // }else{
    //     alert('表單已提交');
    // }
  }
  
  const sendPostRequest = async () => {
    window.location.href = 'http://localhost:8080/ecpayCheckout'
    // axios.post('http://localhost:8080/ecpayCheckout', {})
    //     .then(response => {
    //         responseHTML.value = response.data
    //         document.getElementById('ECpayt').innerHTML = responseHTML.value;
    //         console.log(responseHTML.value)
    //     })
    //     .catch(error => {
    //         console.log(error)
    //     })
  }
  </script>
    
    
    
    <style scoped>
  .login {
    background-color: #f8d479;
    text-align: center;
    height: 100vh;
    display: block; /*顯示  彈性盒子佈局  */
    align-items: center;
    justify-content: center;
    background-image: url('.//config/image/logoicon.png');
    background-size: 100% 100%;
  }
  
  .loginForm {
    display: inline-block;
    vertical-align: middle;
    text-align: center;
    margin-right: 5%;
  }
  
  .dialog-footer button:first-child {
    margin-right: 10px;
  }
  </style>
    