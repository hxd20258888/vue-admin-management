<template>
  <div class="login-wrap">
      <el-form label-position="top" label-width="80px" :model="formData" class="form">
          <h2>用户登录</h2>
  <el-form-item label="用户名">
    <el-input v-model="formData.username"></el-input>
  </el-form-item>
  <el-form-item label="密码">
    <el-input v-model="formData.password"></el-input>
  </el-form-item>
   <el-button type="primary" class="login" @click.prevent="onLogin()">登录</el-button>
</el-form>
  </div>
</template>

<script>
export default {
    data() {
        return {
            formData: {
                username:'',
                paasword:''
            }
        }   
        },
         methods:{
        async onLogin()  {
           const res = await this.$http.post('login',this.formData)
                const {
                    data,
                    meta:{msg,status}
                } = res.data;
                if (status === 200 ) {
                    this.$router.push({ name:'home' });
                    this.$message.success(msg);
                }else {
                    this.$message.error(msg);
                }
        }
    }
}
</script>

<style>
.login-wrap {
    background-color: snow;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-wrap .form {
    width: 400px;
    background-color: #fff;
    border-radius: 5px;
    padding: 30px;
}
.form .login {
    width: 100%;
}
</style>