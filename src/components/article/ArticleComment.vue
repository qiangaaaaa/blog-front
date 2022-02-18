<template>
    <div class="commentInfo">
      <comment-add :receiveArticleId="receiveArticleId" @refreshComments="refreshComments" />
      <div class="commentBody" v-for="comment in comments">
        <comment-group :comment="comment" />
        <el-divider></el-divider>
      </div>
    </div>
  </div>
</template>

<script>
import CommentAdd from "./CommentAdd.vue";
import axios from "axios";
import CommentGroup from './CommentGroup.vue';
export default {
  data() {
    return {
      comments: this.receiveComments,
    };
  },
  methods: {
    refreshComments(articleId) {
      axios
        .get(
          "http://121.199.72.90:9000/blog/comment/" + articleId + "/comments"
        )
        .then((response) => {
          this.comments = response.data.data
        });
    },
  },
  components: { CommentAdd, CommentGroup },
  props: ["receiveArticleId", "receiveComments"],
};
</script>