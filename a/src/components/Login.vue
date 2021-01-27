<template>
<el-container>
    <el-header style="height: 184px"></el-header>
    <el-main>
        <div class="login">
            <el-form :label-position="labelPosition" label-width="80px">
                <h1>学生管理系统</h1>
                <el-form-item label="账号">
                    <el-input v-model="username" placeholder="请输入账号"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                    <el-input placeholder="请输入密码" v-model="password" show-password></el-input>
                </el-form-item>
                <el-button @click="rememberPassword()" style="height: 14px; padding: 0; border: none">
                    <el-checkbox v-model="checked" label-position="left"></el-checkbox>
                    记住密码
                </el-button>
                <br><br>
                <el-button type="primary" @click="register()">注册</el-button>
                <el-button type="success" @click="login()">登录</el-button>
            </el-form>
        </div>
    </el-main>
    <el-footer style="height: 190px"></el-footer>
</el-container>
</template>

<style lang="scss" scoped>
.el-container {
    width: 100%;
    height: 100%;
    background: url("../assets/log.jpg");
    background-repeat: no-repeat;
    background-size: 100%;

    .el-main {
        margin: 0 35%;
        text-align: cneter;

        .login {
            text-align: center;
            width: 400px;
            padding: 10px;
            background-color: white;

        }
    }
}
</style>

<script>
export default {
    data() {
        return {
            labelPosition: 'right',
            username: "",
            password: "",
            dialogFormVisible: false,
            checked: false
        };
    },
    methods: {
        login: function () {
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
                .catch(function (error) {
                    // 请求失败处理
                    console.log(error);
                });
        },
        register: function () {
            this.$router.push({ path: '/register' })
        },
        rememberPassword: function () {
            this.checked = !this.checked;
            if (this.checked == true){
              sessionStorage.setItem("username", this.username);
              sessionStorage.setItem("password", this.password);
            }
        }
    }
};
</script>
