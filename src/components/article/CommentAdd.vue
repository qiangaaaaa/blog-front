<template>
  <div class="commentAdd" style="width:70%">
    <el-form :model="commentAddForm" ref="commentAddForm" label-width="60px">
      <el-row>
        <el-col :span="12">
          <el-form-item prop="email" label="邮箱">
            <el-input v-model="commentAddFormData.email"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item prop="commentNickname" label="昵称">
            <el-input
              v-model="commentAddFormData.commentNickname"
              maxlength="18"
              show-word-limit
            ></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="19">
          <el-form-item prop="content" label="内容">
            <el-input
              type="textarea"
              v-model="commentAddFormData.content"
              maxlength="300"
              show-word-limit
            ></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="5">
          <el-form-item>
            <el-button style="margin-top:8px; " @click="commentPub(commentAddFormData)"
              >评论</el-button
            >
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      commentAddFormData: {
        articleId: this.receiveArticleId,
        content: "",
        commentNickname: "",
        email: "",
      },
    };
  },

  props: ["receiveArticleId"],

  methods: {
    commentPub(commentData) {
      axios
        .post("http://121.199.72.90:9000/blog/comment/save", commentData)
        .then((response) => {
          // 添加评论后刷新评论区
          this.$emit("refreshComments", commentData.articleId);
          console.log(response);
        });
    },
  },
};
</script>

<style>
.el-textarea__inner {
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}
</style>