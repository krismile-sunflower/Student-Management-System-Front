<template>
  <div>
    <h1 style="text-align: center;">学生管理系统</h1>
    <div>
      <el-button type="primary" @click="dialogFormVisible = true"
        >新增</el-button
      >
      <el-button type="danger" @click="delStudent()">删除</el-button>
      <!-- 新增学生信息 -->
      <el-dialog
        title="新增学生信息"
        :visible.sync="dialogFormVisible"
        class="dome"
      >
        <el-form
          :model="form"
          :rules="rules"
          ref="form"
          :inline="true"
          class="demo-form-inline"
        >
          <el-form-item label="学号" :label-width="formLabelWidth" prop="id">
            <el-input v-model="form.id" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="姓名" :label-width="formLabelWidth" prop="name">
            <el-input v-model="form.name" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="性别" prop="sex">
            <el-radio-group v-model="form.sex">
              <el-radio label="女"></el-radio>
              <el-radio label="男"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item
            label="学院"
            :label-width="formLabelWidth"
            prop="college"
          >
            <el-select v-model="form.college" placeholder="请选择学院">
              <el-option
                label="两江人工智能学院"
                value="两江人工智能学院"
              ></el-option>
              <el-option label="理学院" value="理学院"></el-option>
              <el-option label="外国语学院" value="外国语学院"></el-option>
              <el-option label="车辆学院" value="车辆学院"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item
            label="专业"
            :label-width="formLabelWidth"
            prop="profession"
          >
            <el-input v-model="form.profession" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="年级" :label-width="formLabelWidth" prop="grade">
            <el-input v-model="form.grade" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item
            label="班级"
            :label-width="formLabelWidth"
            prop="classes"
          >
            <el-input v-model="form.classes" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="年龄" :label-width="formLabelWidth" prop="age">
            <el-input v-model="form.age" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="爱好" :label-width="formLabelWidth" prop="hobby">
            <el-input v-model="form.hobby" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item style="padding-left: 52px">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="danger" @click="resetForm('form')"
              >重 置</el-button
            >
            <el-button type="primary" @click="addStudent('form')"
              >确 定</el-button
            >
          </el-form-item>
        </el-form>
      </el-dialog>

      <!-- 查看学生信息 -->
      <el-dialog
        title="查看学生信息"
        :visible.sync="dialogFormVisibleCheck"
        class="dome"
      >
        <el-form
          :model="checkForm"
          ref="checkForm"
          :inline="true"
          class="demo-form-inline"
        >
          <el-form-item label="学号" :label-width="formLabelWidth" prop="id">
            <el-input
              v-model="checkForm.id"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item label="姓名" :label-width="formLabelWidth" prop="name">
            <el-input
              v-model="checkForm.name"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item label="性别" prop="sex">
            <el-radio-group v-model="checkForm.sex" disabled>
              <el-radio label="女"></el-radio>
              <el-radio label="男"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item
            label="学院"
            :label-width="formLabelWidth"
            prop="college"
          >
            <el-select
              v-model="checkForm.college"
              placeholder="请选择学院"
              disabled
            >
              <el-option
                label="两江人工智能学院"
                value="两江人工智能学院"
              ></el-option>
              <el-option label="理学院" value="理学院" readonly></el-option>
              <el-option label="外国语学院" value="外国语学院"></el-option>
              <el-option label="车辆学院" value="车辆学院" readonly></el-option>
            </el-select>
          </el-form-item>
          <el-form-item
            label="专业"
            :label-width="formLabelWidth"
            prop="profession"
          >
            <el-input
              v-model="checkForm.profession"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item label="年级" :label-width="formLabelWidth" prop="grade">
            <el-input
              v-model="checkForm.grade"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item
            label="班级"
            :label-width="formLabelWidth"
            prop="classes"
          >
            <el-input
              v-model="checkForm.classes"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item label="年龄" :label-width="formLabelWidth" prop="age">
            <el-input
              v-model="checkForm.age"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item label="爱好" :label-width="formLabelWidth" prop="hobby">
            <el-input
              v-model="checkForm.hobby"
              autocomplete="off"
              disabled
            ></el-input>
          </el-form-item>
          <el-form-item style="padding-left: 52px">
            <el-button @click="dialogFormVisibleCheck = false">取 消</el-button>
            <el-button type="primary" @click="dialogFormVisibleCheck = false"
              >确 定</el-button
            >
          </el-form-item>
        </el-form>
      </el-dialog>

      <!-- 修改学生信息 -->
      <el-dialog
        title="修改学生信息"
        :visible.sync="dialogFormVisibleUpdate"
        class="dome"
      >
        <el-form
          :model="updateForm"
          :rules="rules"
          ref="updateForm"
          :inline="true"
          class="demo-form-inline"
        >
          <el-form-item label="学号" :label-width="formLabelWidth" prop="id">
            <el-input v-model="updateForm.id" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="姓名" :label-width="formLabelWidth" prop="name">
            <el-input v-model="updateForm.name" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="性别" prop="sex">
            <el-radio-group v-model="updateForm.sex">
              <el-radio label="女"></el-radio>
              <el-radio label="男"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item
            label="学院"
            :label-width="formLabelWidth"
            prop="college"
          >
            <el-select v-model="updateForm.college" placeholder="请选择学院">
              <el-option
                label="两江人工智能学院"
                value="两江人工智能学院"
              ></el-option>
              <el-option label="理学院" value="理学院"></el-option>
              <el-option label="外国语学院" value="外国语学院"></el-option>
              <el-option label="车辆学院" value="车辆学院"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item
            label="专业"
            :label-width="formLabelWidth"
            prop="profession"
          >
            <el-input
              v-model="updateForm.profession"
              autocomplete="off"
            ></el-input>
          </el-form-item>
          <el-form-item label="年级" :label-width="formLabelWidth" prop="grade">
            <el-input v-model="updateForm.grade" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item
            label="班级"
            :label-width="formLabelWidth"
            prop="classes"
          >
            <el-input
              v-model="updateForm.classes"
              autocomplete="off"
            ></el-input>
          </el-form-item>
          <el-form-item label="年龄" :label-width="formLabelWidth" prop="age">
            <el-input v-model="updateForm.age" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="爱好" :label-width="formLabelWidth" prop="hobby">
            <el-input v-model="updateForm.hobby" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item style="padding-left: 52px">
            <el-button @click="dialogFormVisibleUpdate = false"
              >取 消</el-button
            >
            <el-button type="danger" @click="resetForm('updateForm')"
              >重 置</el-button
            >
            <el-button type="primary" @click="updateStudent('updateForm')"
              >确 定</el-button
            >
          </el-form-item>
        </el-form>
      </el-dialog>
    </div>
    <!-- 学生信息表格 -->
    <el-table
      ref="multipleTable"
      :current-page="currentPage"
      :page-sizes="[5, 10, 20]"
      :page-size="pageSize"
      :total="students.length"
      :data="
        students.slice((currentPage - 1) * pageSize, currentPage * pageSize)
      "
      :row-class-name="tableRowClassName"
      :row-key="getRowKey"
      tooltip-effect="dark"
      @selection-change="handleSelectionChange"
      @click="getData()"
      style="width: 100%"
    >
      <template>
        <el-table-column
          type="selection"
          width="55"
          :reserve-selection="true"
        ></el-table-column>
        <el-table-column
          prop="number"
          label="序号"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="id"
          label="学号"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="name"
          label="姓名"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="sex"
          label="性别"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="college"
          label="学院"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="profession"
          label="专业"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="grade"
          label="年级"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="classes"
          label="班级"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="age"
          label="年龄"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column
          prop="hobby"
          label="爱好"
          show-overflow-tooltip
        ></el-table-column>
        <el-table-column fixed="right" label="操作" width="100">
          <template slot-scope="scope">
            <el-button @click="check(scope.row)" type="text"
              ><span style="color:red">查看</span></el-button
            >
            <el-button @click="update(scope.row)" type="text"
              ><span style="color:red">修改</span></el-button
            >
          </template>
        </el-table-column>
      </template>
    </el-table>
    <!-- 分页 -->
    <div class="block" style="margin-top:15px;">
      <el-pagination
        align="center"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[5, 10, 20]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="students.length"
      >
      </el-pagination>
    </div>
  </div>
</template>

<style scoped>
.el-dialog__wrapper {
  overflow: hidden;
}
.dome >>> .el-form-item {
  margin-bottom: 20px;
}
.dome >>> .el-form-item__label {
  text-align: left;
  padding: 0;
}
.dome >>> .el-radio-group {
  padding-left: 70px;
  padding-right: 100px;
}
.dome >>> .el-radio__input.is-disabled + span.el-radio__label,
.dome >>> .el-input.is-disabled .el-input__inner {
  color: black;
}
</style>

<script>
// 设置一个全局变量存放学生的长度
var len;
// 设置一个全局变量来存放需要删除学生数组的学号
var b = new Array();

export default {
  data() {
    return {
      students: [],
      currentPage: 1,
      total: 20,
      pageSize: 5,
      dialogFormVisible: false,
      dialogFormVisibleCheck: false,
      dialogFormVisibleUpdate: false,

      form: {
        id: "",
        name: "",
        sex: "女",
        college: [],
        profession: "",
        grade: "",
        classes: "",
        age: "",
        hobby: ""
      },
      checkForm: {
        id: "",
        name: "",
        sex: "女",
        college: [],
        profession: "",
        grade: "",
        classes: "",
        age: "",
        hobby: ""
      },
      updateForm: {
        id: "",
        name: "",
        sex: "女",
        college: [],
        profession: "",
        grade: "",
        classes: "",
        age: "",
        hobby: ""
      },
      formLabelWidth: "100px",
      rules: {
        id: [
          { required: true, message: "请输入学生的学号", trigger: "blur" },
          {
            pattern: /^[0-9]{11}$/,
            message: "学生的学号为11位数字",
            trigger: "blur"
          }
        ],
        name: [
          { required: true, message: "请输入学生的姓名", trigger: "blur" },
          {
            pattern: /^[\u4E00-\u9FA5]{2,5}$/,
            message: "学生姓名不合法",
            trigger: "blur"
          }
        ],
        college: [
          {
            required: true,
            type: "string",
            message: "请选择学生所在学院",
            trigger: "blur"
          }
        ],
        profession: [
          { required: true, message: "请输入学生的专业", trigger: "blur" },
          {
            pattern: /^[\u4E00-\u9FA5]{2,6}$/,
            message: "学生专业不合法",
            trigger: "blur"
          }
        ],
        grade: [
          { required: true, message: "请输入学生的年级", trigger: "blur" },
          {
            pattern: /^[0-9]{2}$/,
            message: "学生的年级为两位数字",
            trigger: "blur"
          }
        ],
        classes: [
          { required: true, message: "请输入学生的班级", trigger: "blur" },
          {
            pattern: /^[0-9]{1,2}$/,
            message: "学生的年级为一到两位数字",
            trigger: "blur"
          }
        ],
        age: [
          { required: true, message: "请输入学生的年龄", trigger: "blur" },
          {
            pattern: /^[0-9]{2}$/,
            message: "学生的年龄为两位数字",
            trigger: "blur"
          }
        ],
        hobby: [
          { required: true, message: "请输入学生的爱好", trigger: "blur" },
          {
            pattern: /^[\u4E00-\u9FA5]{2,6}$/,
            message: "学生的爱好不合法",
            trigger: "blur"
          }
        ]
      }
    };
  },
  created() {
    this.getData();
  },

  methods: {
    getData: function() {
      this.$axios
        .post("http://localhost:8090/student/getAll")
        .then(response => {
          console.log(response.data);
          this.students = response.data;
          len = response.data.length;
        });
    },
    tableRowClassName({ row, rowIndex }) {
      let i = 0;
      if (i < len) {
        for (let j = 1; j <= len / this.pageSize + 1; j++) {
          if (this.currentPage == j) {
            row.number = rowIndex + 1 + (this.currentPage - 1) * this.pageSize;
          }
        }
      }
    },
    check(row) {
      this.$axios
        .put("http://localhost:8090/student/find" + "/" + row.id)
        .then(response => {
          console.log(response.data);
          this.checkForm.id = response.data.id;
          this.checkForm.name = response.data.name;
          this.checkForm.sex = response.data.sex;
          this.checkForm.college = response.data.college;
          this.checkForm.profession = response.data.profession;
          this.checkForm.grade = response.data.grade;
          this.checkForm.classes = response.data.classes;
          this.checkForm.age = response.data.age;
          this.checkForm.hobby = response.data.hobby;
          this.dialogFormVisibleCheck = true;
        });
    },
    update(row) {
      this.$axios
        .put("http://localhost:8090/student/find" + "/" + row.id)
        .then(response => {
          console.log(response.data);
          this.updateForm.id = response.data.id;
          this.updateForm.name = response.data.name;
          this.updateForm.sex = response.data.sex;
          this.updateForm.college = response.data.college;
          this.updateForm.profession = response.data.profession;
          this.updateForm.grade = response.data.grade;
          this.updateForm.classes = response.data.classes;
          this.updateForm.age = response.data.age;
          this.updateForm.hobby = response.data.hobby;
          this.dialogFormVisibleUpdate = true;
        });
    },
    updateStudent: function(updateForm) {
      this.$refs[updateForm].validate(valid => {
        if (valid) {
          this.$axios
            .post("http://localhost:8090/student/update", this.updateForm)
            .then(response => {
              console.log(response.data);
              console.log(this.updateForm.id);
              if (response.data == 200) {
                this.getData();
                this.$message({ message: "修改成功", type: "success" });
              } else this.$message({ message: "修改失败", type: "error" });
            });
          this.dialogFormVisibleUpdate = false;
        } else {
          this.$message({
            message: "修改失败了！",
            type: "error"
          });
          return false;
        }
      });
    },
    addStudent: function(form) {
      this.$refs[form].validate(valid => {
        if (valid) {
          this.$axios
            .post("http://localhost:8090/student/add", this.form)
            .then(response => {
              console.log(response.data);
              console.log(this.form.id);
              if (response.data == 200) {
                this.getData();
                this.$message({ message: "添加成功", type: "success" });
              } else this.$message({ message: "添加失败", type: "error" });
            });
          this.dialogFormVisible = false;
        } else {
          this.$message({
            message: "添加失败了！！",
            type: "error"
          });
          return false;
        }
      });
    },
    delStudent: function(row) {
      console.log(row);
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          for(let i = b.length - 1; i >= 0; i--){
            this.$axios
            .delete("http://localhost:8090/student/delete" + "/" + b[i])
            .then(response => {
              console.log(response.data);
              console.log(this.id);
              this.getData();
            });

          }
          this.$message({
            type: "success",
            message: "删除成功!"
          })
          
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    getRowKey(row) {
      return row.id;
    },

    handleSelectionChange(val) {
      let j = val.length - 1;
      for (let i = val.length - 1; i >= 0; i--, j--) {
        b[j] = val[i].id;
      }
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },

    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
      this.currentPage = 1;
      this.pageSize = val;
    },

    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.currentPage = val;
    }
  },
};
</script>
