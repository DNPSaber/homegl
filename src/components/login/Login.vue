<script setup>
import Storage from '../../tools/Storage'
import { ElMessage } from 'element-plus'
import { ref, computed } from 'vue'
import {useRouter} from 'vue-router'
const store = Storage()
const router = useRouter()
// 用户名和密码
const name = ref("")
const password = ref("")
const disabled = computed(()=>{
    return name.value.length == 0 || password.value.length == 0;
}) 
// 用户登录的方法
function login() {
    store.registUserInfo(name.value, password.value)
    ElMessage({
        message:'登录成功', 
        type:'success', 
        duration:3000
    })
    setTimeout(() => {
        router.push({name:"home"})
    }, 3000);
}
</script>
<template>
    <div id="container">
        <div id="title">
            <h1>dnpsaber电商后台</h1>
        </div>
        <div class="input">
            <el-input v-model="name" prefix-icon="User" placeholder="请输入用户名"></el-input>
        </div>
        <div class="input">
            <el-input v-model="password" prefix-icon="Lock" placeholder="请输入密码" auto-complete="new-password" show-password></el-input>
        </div>
        <div class="input">
            <el-button @click="login" style="width:500px" type="primary" :disabled="disabled">登录</el-button>
        </div>
    </div>
</template>
<style scoped>
#container {
    background: #595959;
    background-image: url("/public/login_bg.jpg");
    background-size: cover;
    background-position: center;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
#title {
    text-align: center;
    color: azure;
    margin-bottom: 20px;
}
.input {
    margin: 10px 0;
    width: 100%;
    max-width: 500px;
    padding: 0 20px;
}
</style>
