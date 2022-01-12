<template>
  <!--文章详情-->
  <div class="articleDetail"
       v-loading="loading"
       element-loading-background="rgba(0, 0, 0, 0.6)">
    <!--文章信息-->
    <div class="articleInfo">
      <!--文章头部信息-->
      <div class="articleHeader">
        <h1 class="title">
          {{ articleDetail.title }}
        </h1>
        <!--文章标签-->
        <div class="label">
          <el-tag v-for="label in articleDetail.labels" type="success" :labelId="label.labelId"
                  size="mini" :title="label.description">
            {{ label.labelName }}
          </el-tag>
          <!--</el-tooltip>-->
        </div>
        <!--文章分类-->
        <div class="category">
          <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item>{{ articleDetail.category.categoryName }}</el-breadcrumb-item>
            <el-breadcrumb-item>{{ articleDetail.category.subCategory.categoryName }}</el-breadcrumb-item>
          </el-breadcrumb>
        </div>
      </div>
      <!--文章主体内容-->
      <div class="articleBody" v-html="articleContent"></div>
    </div>
    <!--文章评论信息-->
    <div class="commentInfo">
      <div class="commentBody"
           v-for="comment in articleDetail.comments">
        <!--评论-->
        <div class="comment">
          <span>{{ comment.commentNickname }}</span>
          <span>{{ comment.commentTime }}</span>
          <p class="comment">{{ comment.content }}</p>
          <!--回复-->
          <div class="replyBody"
               v-for="reply in comment.replyResponseVOS">
            <span>{{ reply.replyNickname }}</span>
            <span v-if="reply.parentReplyId != 0"> 回复 {{ reply.targetNickName }}</span>
            <br>
            <span>{{ reply.content }}</span>
            <p>{{ reply.replyTime }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import showdown from "showdown";

export default {
  data() {
    return {
      loading: true,
      articleContent: null,
      articleDetail: null
    };
  },
  methods: {
    getListDetail() {
      axios
        .get(
          // "http://localhost:9000/blog/article/info/" + this.$route.params.id
          "http://121.199.72.90:9000/blog/article/info/" + this.$route.params.id
        )
        .then((response) => {
          console.log(response)
          this.articleDetail = response.data.data;
          let converter = new showdown.Converter();
          this.articleContent = converter.makeHtml(this.articleDetail.content);
          this.loading = false
        });
    },
  },
  mounted() {
    this.getListDetail();
  },
}
</script>
