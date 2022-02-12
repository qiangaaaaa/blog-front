<template>
  <div class="commentAdd">
    <el-form
      :model="commentAddForm"
      :inline="true"
      ref="commentAddForm"
      label-width="60px"
    >
      <el-form-item
        prop="email"
        label="邮箱"
        :rules="[
          { required: true, message: '请输入邮箱地址', trigger: 'blur' },
          {
            type: 'email',
            message: '请输入正确的邮箱地址',
            trigger: ['blur', 'change'],
          },
        ]"
      >
        <el-input v-model="commentAddFormData.email"></el-input>
      </el-form-item>
      <el-form-item prop="commentNickname" label="昵称" required="true">
        <el-input
          v-model="commentAddFormData.commentNickname"
          maxlength="18"
          show-word-limit
        ></el-input>
      </el-form-item>
      <el-form-item prop="content" label="评论内容" required="">
        <el-input
          type="textarea"
          v-model="commentAddFormData.content"
          maxlength="300"
          show-word-limit
        ></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="commentPub(commentAddFormData)"
          >评论</el-button
        >
      </el-form-item>
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
        .post(
          "http://121.199.72.90:9000/blog/comment/save",commentData
        )
        .then((response) => {
          // 添加评论后刷新评论区
          this.$emit("refreshComments", commentData.articleId)
          console.log(response);
        });
    },
  },
};
</script>

<style>
.commentAdd {
  border: 1px solid rgba(0, 0, 0, 0.6);
}
</style>