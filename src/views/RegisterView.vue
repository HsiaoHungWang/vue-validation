
<template>
  <div class="row">
    <div class="col-3"></div>
    <div class="col-6">
      <h2>驗證範例</h2>
      <p>統一顯示所有的驗證錯誤訊息</p>
      <form id="registerForm" @submit.prevent="validate()" novalidate class="mb-3">
        <div class="input-group mb-3">
          <label for="account" class="input-group-text">帳號</label>
          <input type="text" v-model="registerData.account" class="form-control" id="account" required autofocus
            autocomplete="off">
        </div>
        <div class="input-group mb-3">
          <label for="pwd1" class="input-group-text">密碼</label>
          <input type="password" v-model="registerData.pwd1" class="form-control" id="pwd1" autocomplete="off">
        </div>
        <div class="input-group mb-3">
          <label for="pwd2" class="input-group-text">密碼確認</label>
          <input type="password" v-model="registerData.pwd2" class="form-control" id="pwd2" autocomplete="off">
        </div>

        <div class="input-group mb-3">
          <label for="email" class="input-group-text">電子郵件</label>
          <input type="email" v-model="registerData.email" class="form-control" id="email">
        </div>


        <button type="submit" class="btn btn-primary" id="buttonSubmit">送出</button>

      </form>
      <ul class="list-group">
        <li v-for="(value, index) in errorMessage" :key="index" class="list-group-item list-group-item-warning">
          {{ value }}
        </li>
      </ul>
    </div>
    <div class="col-3">

    </div>
  </div>
</template>

<style></style>
<script setup>
import { reactive, computed } from 'vue'
const registerData = reactive({
  "account": "",
  "pwd1": "",
  "pwd2": "",
  "email": ""
});

const errorMessage = reactive([]);
const emailRule = /^[^@\s]+@[^@\s]+\.[^@\s]+$/;
// console.log(emailRule.test("abc@company.com")) //true
// console.log(emailRule.test("@company.com")) //false
// console.log(emailRule.test("abc@company"))  //false


// // Define computed properties for form validation
// const isAccountValid = computed(() => {
//   console.log(registerData.account)
//   return registerData.account.length > 0
// });
// // const isValidLastName = computed(() => formData.lastName.length > 0);
// const isValid = computed(() => isAccountValid.value);


const validate = () => {
  const { account, pwd1, pwd2, email } = registerData;
  errorMessage.length = 0;
  if (account.length === 0) {
    errorMessage.push("帳號一定要輸入")
  }
  if (pwd1.length === 0) {
    errorMessage.push("密碼一定要輸入")
  } else if (pwd1 !== pwd2) {
    errorMessage.push("密碼不一致")
  }
  if (email.length === 0) {
    errorMessage.push("電子郵件要輸入")
  } else if (!emailRule.test(email)) {
    errorMessage.push("電子郵件格式不正確")
  }
  if (errorMessage.length === 0) {
    //將 registerData 中的資料送到Server端
    console.log(registerData);
  }


}
</script>
