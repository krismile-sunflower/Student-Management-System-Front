<template>
  <div id="center">
    <el-form :model="form" :rules="rules">
      <el-form-item label="账号" :label-width="formLabelWidth" prop="username">
        <el-input v-model="form.username" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="密码" :label-width="formLabelWidth" prop="password">
        <el-input
          v-model="form.password"
          autocomplete="off"
          show-password
        ></el-input>
      </el-form-item>
    </el-form>
    <el-form :model="checkForm">
      <el-form-item label="确认密码" :label-width="formLabelWidth">
        <el-input
          v-model="checkForm.checkPassword"
          autocomplete="off"
          show-password
        ></el-input>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="cancle()">取 消</el-button>
      <el-button type="primary" @click="register()">确 定</el-button>
    </div>
  </div>
</template>

<style>
#center {
  width: 500px;
  margin: 0 auto;
  margin-top: 200px;
}
.dialog-footer {
  padding-left: 320px;
}
</style>

<script>
export default {
  data() {
    return {
      form: {
        username: "",
        password: ""
      },
      checkForm: {
        checkPassword: ""
      },
      formLabelWidth: "80px",
      rules: {
          username: [
            { required: true, message: '请输入你的用户名', trigger: 'blur' },
          ],
          password: [
             { required: true, message: '请输入你的密码', trigger: 'blur' },
             { min: 5, message: '长度至少为 5 个字符', trigger: 'blur' }
          ]
        }
    };
  },
  methods: {
    cancle: function() {
      this.$router.push({ path: "/" });
    },
    register: function() {
      console.log(this.form.username);
      console.log(this.form.password);
      console.log(this.checkForm.checkPassword);
      if (this.form.password != this.checkForm.checkPassword) {
        this.$message({ message: "输入的密码不一致", type: "error" });
        return;
      }
      this.$axios
        .post("http://localhost:8090/user/add", this.form)
        .then(response => {
          console.log(response.data);
          if (response.data == 2) {
            this.$message({ message: "该用户名已经被注册", type: "error" });
          } else if (response.data == 0) {
            this.$message({ message: "该用户名不能为空", type: "error" });
          } else if (response.data == 1) {
            this.$alert("注册成功", {
              confirmButtonText: "确定",
              callback: action => {
                console.log(action);
                this.$message({
                  type: "success",
                  message: "现在你已经注册了账号"
                });
                this.$router.push({ path: "/" });
              }
            });
          }
        });
    }
  }
};
</script>