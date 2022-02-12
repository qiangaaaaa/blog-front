<template>
  <div class="articleHeader">
    <h1 class="title">
      {{ title }}
    </h1>
    <!--文章标签-->
    <div class="label">
      <el-tag
        v-for="label in labels"
        type="success"
        :labelId="label.labelId"
        size="mini"
        :title="label.description"
      >
        {{ label.labelName }}
      </el-tag>
      <!--</el-tooltip>-->
    </div>
    <!--文章分类-->
    <div class="category">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item>{{ category.categoryName }}</el-breadcrumb-item>
        <el-breadcrumb-item>{{
          category.subCategory.categoryName
        }}</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!-- 时间 -->
    <div class="time">
      <p>最后修改于: {{ publishTime }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["title", "labels", "category", "publishTime"],
};
</script>