<template>
  <div class="login">
        <i-form ref="formLogin" :model="formLogin" :rules="ruleLoginRules"  class="card-box" >
                <!-- title -->
            <FormItem class="formLogin-title">
                <h3>系统登陆</h3>
            </FormItem>
            <FormItem prop="username">
                <i-input size="large" type="text" v-model="formLogin.username" placeholder="用户名">
                    <Icon type="ios-person-outline" slot="prepend"></Icon>
                </i-input>
            </FormItem>
            <FormItem prop="password">
                <i-input size="large" type="password" v-model="formLogin.password" placeholder="密码">
                    <Icon type="ios-lock-outline" slot="prepend"></Icon>
                </i-input>
            </FormItem>
            <FormItem class="login-no-bottom">
                <Checkbox v-model="formLogin.remeber">记住密码</Checkbox>
            </FormItem>
            <FormItem>
                <Row> 
                    <Col :xs = "{ span: 4, offset: 6}">
                        <Button type="primary" @click="handleSubmit('formLogin')">登陆</Button>
                    </Col>
                    <Col :xs = "{ span: 6, offset: 4}">
                        <Button type="primary" @click="formLoginReset('formLogin')">重置</Button>
                    </Col>
                </Row>
            </FormItem>
        </i-form>
  </div>
</template>
<script>
export default {
  name: 'Login',
  data () {
    return {
        formLogin:{
            username: '',
            password: '',
            remeber: false
        },
        ruleLoginRules: {
                username: [
                    { required: true, message: 'Please fill in the user name', trigger: 'blur' }
                ],
                password: [
                    { required: true, message: 'Please fill in the password.', trigger: 'blur' },
                    { type: 'string', min: 6, message: 'The password length cannot be less than 6 bits', trigger: 'blur' }
                ]
            }
        }
  },
  methods: {
      handleSubmit (name){
          this.$refs[name].validate( valid => {
              sessionStorage.setItem('user', JSON.stringify(this.formLogin.username))
              if (valid) {
                  this.$Message.success('提交成功'),
                  this.$router.push({path:'/home'})
              }else {
                  this.$Message.error('登陆失败')
              }
              if (this.formLogin.remeber) {
                  sessionStorage.setItem('username', JSON.stringify(this.formLogin.username))
                  sessionStorage.setItem('password', JSON.stringify(this.formLogin.password))
              } else {
                  sessionStorage.removeItem('username')
                  sessionStorage.removeItem('password')
              }
          })
      }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .login {
        width: 100%;
        height: 100%;
        background: url(../assets/bg.jpg)  no-repeat;
        background-size: cover;
        overflow: hidden;
    }
    .card-box {
        padding: 20px;
        /*box-shadow: 0 0px 8px 0 rgba(0, 0, 0, 0.06), 0 1px 0px 0 rgba(0, 0, 0, 0.02);*/
        -webkit-border-radius: 5px;
        border-radius: 5px;
        -moz-border-radius: 5px;
        background-clip: padding-box;
        margin-bottom: 20px;
        background-color: #f9fafc;
        margin: 180px auto;
        width: 400px;
        border: 2px solid #8492a6;
    }

    .title {
        margin: 0px auto 40px auto;
        text-align: center;
        color: #505458;
    }
    .formLogin-title {
        text-align: center;
        font-size: 28px;
    }
    .formLogin-title h3 {
        font-size: 18px;
    }
    /* .ivu-form-item-content{
        display: flex;
        justify-content: flex-start;
    } */
    .login-no-bottom {
        margin-bottom: 10px;
        margin-right: 280px;
    }
    .ivu-checkbox-wrapper{
        margin-right: 0;
    }
</style>
