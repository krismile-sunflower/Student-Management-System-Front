<template>
  <div>
    <div id="enter">
      <h1>学生管理系统</h1>
      <el-input v-model="username" placeholder="请输入账号"></el-input>
      <br /><br />
      <el-input
        placeholder="请输入密码"
        v-model="password"
        show-password
      ></el-input>
      <br /><br />
      <el-button type="primary" style="margin-left: 120px" @click="register()"
        >注册</el-button
      >
      <el-button type="success" @click="login()">登录</el-button>
    </div>
  </div>
</template>

<style>
body {
  background-color: aqua;
  background-repeat: no-repeat;
  background-size: 100%;
}
#enter {
  height: 200px;
  width: 280px;
  margin: 250px auto;
}
</style>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      dialogFormVisible: false,
    };
  },
  methods: {
    login: function() {
      this.$axios
        .get("http://localhost:8090/user/login", {
          params: { username: this.username, password: this.password }
        })
        .then(response => {
          console.log(response.data);
          console.log(this.username);
          if (response.data === "ok") {
            localStorage.setItem("username", this.username);
            localStorage.setItem("password", this.password);
            localStorage.setItem("status", "ok");
            this.$message("登陆成功");
            window.location.href = "/student";
          } else if (response.data === "error username") {
            this.$message("用户名错误");
          } else if (response.data === "error password") {
            this.$message("密码错误");
          }
        })
        .catch(function(error) {
          // 请求失败处理
          console.log(error);
        });
    },
    register: function() {
      this.$router.push({path:'/register'})
    }
  }
};
</script>

