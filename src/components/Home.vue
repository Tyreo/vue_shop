<template>
    <div class="home-container">
        <el-button type="info" @click="loginOut">退出</el-button>
    </div>
</template>
<script>
export default {
  data () {
    return {
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      loginRules: {
        username: [
          {
            required: true,
            message: '请输入登录名',
            trigger: 'blur'
          },
          {
            min: 3,
            max: 10,
            message: '长度在3到10个字符',
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: '请输入登录密码',
            trigger: 'blur'
          },
          {
            min: 6,
            max: 12,
            message: '长度在6到12个字符',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    loginOut () {
      sessionStorage.clear('TOKEN')
      this.$router.push('/login')
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
