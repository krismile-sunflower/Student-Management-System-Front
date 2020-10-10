<template>
  <div id="app">
    <!-- <div id="nav">
      <el-button type="primary"> <router-link to="/student">学生管理系统</router-link></el-button>
      <el-button type="primary"> <router-link to="/teacher">教师管理系统</router-link></el-button>
    </div>
    <router-view/> -->
    <!-- <Student></Student> -->
    <div class="left">
      <el-row class="tac">
        <el-col :span="3">
          <el-menu default-active="2" class="el-menu-vertical-demo">
            <el-menu-item index="1">
              <i class="el-icon-menu"></i>
              <span slot="title"
                ><router-link to="/teacher">教师管理系统</router-link></span
              >
            </el-menu-item>

            <el-menu-item index="2">
              <i class="el-icon-menu"></i>
              <span slot="title"
                ><router-link to="/student">学生管理系统</router-link></span
              >
            </el-menu-item>
            <el-menu-item index="3" disabled>
              <i class="el-icon-document"></i>
              <span slot="title">教务处</span>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </div>

    <div class="right">
      <router-view />
    </div>
  </div>
</template>


<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 1500px;
  margin: 0 auto;
}
a {
  text-decoration: none;
  display: inline-block;
  width: 100px;
}
.left {
  float: left;
  width: 200px;
  margin-top: 60px;
}
.right {
  float: left;
  width: 1300px;
}
</style>

