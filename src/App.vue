<template>
  <div id="app">
    <el-container>
      <!--头部-->
      <el-header height="300px">
        <blog-header />
      </el-header>
      <!--主体-->
      <el-main>
        <el-row>
          <!--跳转：事件总线-->
          <!--左侧-->
          <el-col :span="3">
            <div class="grid-content bg-purple">left</div>
          </el-col>
          <!--内容区-->
          <el-col :span="14">
            <router-view />
          </el-col>
          <!--右侧-->
          <el-col :span="7">
            <div class="grid-content bg-purple">right1</div>
          </el-col>
        </el-row>
      </el-main>
      <!--底部-->
      <el-footer> footer </el-footer>
    </el-container>
  </div>
</template>

<script>
import BlogHeader from "./components/blogHeader/BlogHeader";

export default {
  components: { BlogHeader },
  name: "App",
};
</script>

<style>
</style>
