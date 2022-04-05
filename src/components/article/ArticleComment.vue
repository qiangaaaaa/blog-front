<template>
  <div class="commentInfo">
    <comment-and-reply-add :receiveArticleId="receiveArticleId" :receiveContent="defaultContent" @refreshComments="refreshComments" :receiveType="0" />
    <div class="commentBody" v-for="comment in comments">
      <comment-group :comment="comment" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CommentGroup from "./CommentGroup.vue";
import CommentAndReplyAdd from "./CommentAndReplyAdd.vue";
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
          this.comments = response.data.data;
        });
    },
  },
  components: { CommentGroup, CommentAndReplyAdd },
  props: ["receiveArticleId", "receiveComments"],
};
</script>
