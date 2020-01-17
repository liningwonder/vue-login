<template>
    <el-form :model="loginForm" :rules="fieldRules" ref="loginForm" label-position="left" label-width="0px" class="demo-ruleForm login-container">
        <span class="tool-bar">
        </span>
        <h2 class="title" style="padding-left:22px;" >系统登录</h2>
        <el-form-item prop="account">
            <el-input type="text" v-model="loginForm.account" auto-complete="off" placeholder="账号"></el-input>
        </el-form-item>
        <el-form-item prop="password">
            <el-input type="password" v-model="loginForm.password" auto-complete="off" placeholder="密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-col :span="12">
            <el-form-item prop="captcha">
              <el-input type="test" v-model="loginForm.captcha" auto-complete="off" placeholder="验证码, 单击图片刷新"
                style="width: 100%;">
              </el-input>
            </el-form-item>
          </el-col>
          <el-col class="line" :span="1">&nbsp;</el-col>
          <el-col :span="11">
            <el-form-item>
              <img style="width: 100%;" class="pointer" :src="loginForm.src" @click="refreshCaptcha">
            </el-form-item>
          </el-col>
        </el-form-item>
        <el-form-item style="width:100%;">
          <el-button type="primary" style="width:48%;" @click.native.prevent="reset">重 置</el-button>
          <el-button type="primary" style="width:48%;" @click.native.prevent="login" :loading="loading">登 录</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
export default {
   name: 'Login',
   data() {
    return {
      loading: false,
      loginForm: {
        account: '',
        password: '',
        captcha:'',
        src: ''
      },
      fieldRules: {
        account: [
          { required: true, message: '请输入账号', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' }
        ]
      },
      checked: true
    }
  },
  methods: {
    login() {
      this.loading = true
      let userInfo = { account:this.loginForm.account, password:this.loginForm.password, captcha:this.loginForm.captcha }
      console.log("login test")
      this.axios.post('http://localhost:8001/login', {account:this.loginForm.account,captcha:this.loginForm.captcha,password:this.loginForm.password}).then(response => {
        //console.log('response' + response)
        //console.log('body' + response.body)
        //console.log('data' + response.data)
        //console.log('code' + response.data.code)
        if (response.data.code == 200) {
          this.$router.push('/')
        } else {
          //alert(response.data.msg)
          this.$message({message: response.data.msg, type: 'error'})
        }
        //this.$router.push('/')
      }).catch(error => {
        console.log(error);
        this.$message({message: 'unknown error', type: 'error'})
      })
      this.loading = false
    },
    refreshCaptcha() {
      console.log("axios test")
      this.axios.get('http://localhost:8001/captcha.jpg', {responseType: 'arraybuffer'}).then(response => {
        console.log(response)
        this.loginForm.src = 'data:image/png;base64,' + btoa(new Uint8Array(response.data).reduce((data,byte) => data + String.fromCharCode(byte), ''))
      })
    },
    reset() {
      this.$refs['loginForm'].resetFields()
    }
  },
  mounted() {
    this.refreshCaptcha()
  }
}
</script>

<style lang="scss" scoped>
  .login-container {
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin: 100px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
    .title {
      margin: 0px auto 30px auto;
      text-align: center;
      color: #505458;
    }
  }
</style>