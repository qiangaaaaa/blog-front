<template>
  <!--文章详情-->
  <div
    class="articleDetail1"
    v-loading="loading"
    element-loading-background="rgba(0, 0, 0, 0.6)"
  >
    <!-- 文章头部 -->
    <article-header
      :title="articleDetail.title"
      :labels="articleDetail.labels"
      :category="articleDetail.category"
      :publishTime="articleDetail.publishTime"
    />

    <!--文章内容-->
    <article-body :articleBody="articleContent" />

    <!--文章评论-->
    <article-comment :receiveArticleId="articleDetail.articleId" :receiveComments="articleDetail.comments" />
  </div>
</template>

<script>
import axios from "axios";
import showdown from "showdown";
import ArticleBody from "../article/ArticleBody.vue";
import ArticleComment from "../article/ArticleComment.vue";
import ArticleHeader from "../article/ArticleHeader.vue";

export default {
  components: { ArticleBody, ArticleComment, ArticleHeader },
  data() {
    return {
      loading: true,
      articleContent: null,
      articleDetail: null,
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
          console.log(response);
          this.articleDetail = response.data.data;
          let converter = new showdown.Converter();
          this.articleContent = converter.makeHtml(this.articleDetail.content);
          this.loading = false;
        });
    },
  },
  mounted() {
    this.getListDetail();
  },
};
</script>
