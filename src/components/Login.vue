<template>
    <div class="login-container">
        <div class="login-box">
            <div class="avatar-box">
                <img src="../assets/logo.png" alt="">
            </div>
        <el-form v-model="loginForm" label-width="0px" class="form-box">
            <el-form-item>
                <el-input v-model="loginForm.username" prefix-icon="iconfont icon-user"></el-input>
            </el-form-item>
            <el-form-item>
                <el-input v-model="loginForm.password" type="password" prefix-icon="iconfont icon-3702mima"></el-input>
            </el-form-item>
            <el-form-item class="btns">
                <el-button type="primary" >登陆</el-button>
                <el-button type="info" >重置</el-button>
            </el-form-item>
        </el-form>
        </div>
    </div>
</template>
<script>
export default {
  data () {
    return {
      loginForm: {
        username: '2345',
        password: '5454'
      }
    }
  }
}
</script>
<style lang="less" scoped>
    .login-container {
        height: 100%;
        background-color: #2b4b6b;
    }
    .login-box {
        width: 450px;
        height: 300px;
        background-color: #fff;
        border-radius: 3px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
    .avatar-box {
        height: 130px;
        width: 130px;
        border: 1px solid #eee;
        border-radius: 50%;
        padding: 10px;
        box-shadow: 0 0 10px #ddd;
        position: absolute;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: #fff;
        img {
            height: 100%;
            width: 100%;
            border-radius: 50%;
            background-color: #eee;
        }
    }
    .form-box {
        position: absolute;
        left: 0;
        top: 100px;
        padding: 20px;
        box-sizing: border-box;
        width: 100%;
    }
    .btns {
        display: flex;
        justify-content: flex-end;
    }
</style>
