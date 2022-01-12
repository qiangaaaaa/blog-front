<template>
  <div id="app">
    <el-container>
      <!--header-->
      <el-header height="300px">
        <blog-header/>
      </el-header>
      <!--main-->
      <el-main>
        <el-row>
          <!--left-->
          <el-col :span="3">
            <div class="grid-content bg-purple">left</div>
          </el-col>
          <!--center-->
          <el-col :span="14">
            <router-view/>
          </el-col>
          <!--right-->
          <el-col :span="4">
            <div class="grid-content bg-purple">right1</div>
          </el-col>
          <el-col :span="3">
            <div class="grid-content bg-purple">right2</div>
          </el-col>
        </el-row>
      </el-main>
      <!--footer-->
      <el-footer>
        footer
      </el-footer>
    </el-container>

  </div>
</template>

<script>
import ArticleList from "./components/articleList/ArticleList.vue";
import ArticleDetail from "./components/articleDetail/ArticleDetail";
import BlogHeader from "./components/blogHeader/BlogHeader";

export default {
  components: {BlogHeader, ArticleList, ArticleDetail},
  name: "App",
};
</script>

<style>
.grid-content {
  /*background-color: #232323;*/
}
</style>
