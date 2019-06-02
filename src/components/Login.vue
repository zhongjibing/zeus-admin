<template>
  <div class="page-responsive session-authentication intent-mouse">
    <div class="main">
      <form class="form-login" action="http://localhost:8080/login" method="post">
        <h2 class="form-login-header">Please login</h2>
        <div v-if="param.error">
          Incorrect username or password.
        </div>
        <div v-if="param.logout">
          You have been logged out.
        </div>
        <input type="text" class="form-control" name="username" placeholder="Username or email address" required="" autofocus="" />
        <input type="password" class="form-control" name="password" placeholder="Password" required=""/>
        <label class="checkbox">
          <input type="checkbox" value="remember-me" id="rememberMe" name="rememberMe"/> Remember me
          <a href="/password_reset" class="label-link">Forgot password?</a>
        </label>
        <label class="checkbox">
          <el-checkbox v-model="checked">备选项</el-checkbox>
          <a href="/password_reset" class="label-link">Forgot password?</a>
        </label>
        <button class="btn btn-lg btn-primary btn-block" type="submit">Login</button>
        <p class="create-account-callout mt-3">
          <a href="/join">Create an account</a>.
        </p>
        <el-button v-on:click="sub" type="primary">sub</el-button>
      </form>
    </div>
  </div>
</template>

<script>

  import axios from 'axios'
  import request from '../../config/request'

  export default {
    name: 'Login',
    data () {
      return {
        checked: false,
        param: {
          error: false,
          logout: false
        }
      }
    },
    mounted() {
    },
    methods: {
      sub: function() {
        let requestUrl = request.REQUEST + '/hello'
        axios({
          method: 'get',
          url: requestUrl,
          heasers: {'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8'},
          params: {'name':'123'}
        })
          .then(function (res) {
            console.log(res.data)
          })
          .catch(function (err) {
            console.log(err)
          })


      }
    }
  }
</script>
<style scoped>
  @import "../../static/css/login.css";
</style>
