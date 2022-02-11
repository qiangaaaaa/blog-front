<template>
  <div id="app">
    <el-container>
      <!--头部-->
      <el-header height="800px">
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
import ArticleList from "./components/articleList/ArticleList.vue";
import ArticleDetail from "./components/articleDetail/ArticleDetail";
import BlogHeader from "./components/blogHeader/BlogHeader";

export default {
  components: { BlogHeader, ArticleList, ArticleDetail },
  name: "App",
};
</script>

<style>
</style>
