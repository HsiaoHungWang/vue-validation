
<template>
  <div class="row">
    <div class="col-3"></div>
    <div class="col-6">
      <h2>驗證範例</h2>
      <p>錯誤訊息顯示在每一個文字輸入方塊的下面</p>
      <form id="registerForm" @submit.prevent="validate()" novalidate>
        <div class="input-group">
          <label for="account" class="input-group-text">帳號</label>
          <input type="text" v-model="registerData.account" class="form-control" id="account" required autofocus
            autocomplete="off">
          <span v-if="!validity.accountRequired" class="input-group-text bg-danger text-white"><i
              class="bi bi-x-lg"></i></span>
        </div>
        <div class="mb-3"><small v-if="!validity.accountRequired" class="text-danger">帳號一定要輸入</small></div>
        <div class="input-group">
          <label for="pwd1" class="input-group-text">密碼</label>
          <input type="password" v-model="registerData.pwd1" class="form-control" id="pwd1" autocomplete="off">
          <span v-if="!validity.pwdRequired" class="input-group-text bg-danger text-white"><i
              class="bi bi-x-lg"></i></span>
        </div>
        <div class="mb-3"><small v-if="!validity.pwdRequired" class="text-danger">密碼一定要輸入</small></div>

        <div class="input-group">
          <label for="pwd2" class="input-group-text">密碼確認</label>
          <input type="password" v-model="registerData.pwd2" class="form-control" id="pwd2" autocomplete="off">
          <span v-if="!validity.pwdConfirm" class="input-group-text bg-danger text-white hide"><i
              class="bi bi-x-lg"></i></span>
        </div>
        <div class="mb-3">
          <small class="text-danger hide" v-if="!validity.pwdConfirm">密碼不一致</small>
        </div>
        <div class="input-group">
          <label for="email" class="input-group-text">電子郵件</label>
          <input type="email" v-model="registerData.email" class="form-control" id="email">
          <span v-if="!validity.emailRequired || !validity.emailFormat" class="input-group-text bg-danger text-white"><i
              class="bi bi-x-lg"></i></span>
        </div>
        <div class="mb-3">
          <small v-if="!validity.emailRequired" class="text-danger">電子郵件要輸入</small><br>
          <small v-if="!validity.emailFormat" class="text-danger">電子郵件格式不正確</small>
        </div>

        <button type="submit" class="btn btn-primary" id="buttonSubmit">送出</button>

      </form>

    </div>
    <div class="col-3">

    </div>
  </div>
</template>

<style></style>
<script setup>
import { reactive, computed, ref } from 'vue'
const registerData = reactive({
  "account": "",
  "pwd1": "",
  "pwd2": "",
  "email": ""
})

const validity = reactive({
  "accountRequired": true,
  "pwdRequired": true,
  "pwdConfirm": true,
  "emailRequired": true,
  "emailFormat": true,
  "isValid": false
})

const emailRule = /^[^@\s]+@[^@\s]+\.[^@\s]+$/;
// console.log(emailRule.test("abc@company.com")) //true
// console.log(emailRule.test("@company.com")) //false
// console.log(emailRule.test("abc@company"))  //false



const validate = () => {
  const { account, pwd1, pwd2, email } = registerData;

  validity.accountRequired = account.length > 0
  validity.pwdRequired = pwd1.length > 0
  validity.pwdConfirm = pwd1 === pwd2
  validity.emailRequired = email.length > 0
  validity.emailFormat = emailRule.test(email)

  validity.isValid = validity.accountRequired && validity.pwdRequired && validity.pwdConfirm && validity.emailRequired && validity.emailFormat



  if (validity.isValid) {
    //將 registerData 中的資料送到Server端
    console.log(registerData);
  }


}
</script>
