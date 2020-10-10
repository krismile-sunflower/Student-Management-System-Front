<template>
  <div>
    <h1 style="text-align: center;">教师管理系统</h1>

    <el-table
      :data="tableData"
      style="width: 100%"
      :row-class-name="tableRowClassName"
    >
      <el-table-column label="序号" type='index' width="100"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
      <el-table-column prop="sex" label="性别" width="180"> </el-table-column>
      <el-table-column prop="subject" label="学科" width="180"> </el-table-column>
       <el-table-column prop="telephone" label="电话号码" > </el-table-column>
    </el-table>
  </div>
</template>




<style>
.el-table .warning-row {
  background: oldlace;
}

.el-table .success-row {
  background: #f0f9eb;
}
</style>
<script>
export default {
  methods: {
    tableRowClassName({ row, rowIndex }) {
      console.log(row);
      if (rowIndex === 1) {
        return "warning-row";
      } else if (rowIndex === 3) {
        return "success-row";
      }
      return "";
    }
  },
  data() {
    return {
      tableData: [
        {
          name: "张世坤",
          sex: "男",
          subject: "C语言程序设计",
          telephone: 17143812423
        },
        {
          name: "李思",
          sex: "女",
          subject: "大学英语",
          telephone: 17492534729
        },
        {
          name: "李胜男",
          sex: "男",
          subject: "大学物理",
          telephone: 17236348626
        },
        {
          name: "王寿康",
          sex: "男",
          subject: "形势与政策",
          telephone: 17492524753
        }
      ]
    };
  }
};
</script>