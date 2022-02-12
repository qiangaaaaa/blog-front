<template>
  <div class="commentGroup">
    <!--评论-->
    <div class="comment">
      <span>{{ comment.commentNickname }}</span>
      <span>{{ comment.commentTime }}</span>
      <p class="content">{{ comment.content }}</p>
    </div>
    <!--回复-->
    <div class="reply">
      <div class="replyBody" v-for="reply in comment.replyResponseVOS">
        <span>{{ reply.replyNickname }}</span>
        <span v-if="reply.parentReplyId != 0">
          回复 {{ reply.targetNickName }}</span
        >
        <span>{{ reply.replyTime }}</span>
        <br />
        <p>{{ reply.content }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },

  props: ["comment"],

  components: {},

  computed: {},

  mounted: {},

  methods: {},
};
</script>

<style>
.commentGroup {
  border-bottom: 1px solid black;
  margin-bottom: 2px;
}
.commentGroup::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
}
.comment {
  background-color: rgb(87, 87, 87);
}
.reply {
  background-color: rgb(133, 133, 133);
  float: right;
  width: 95%;
}
</style>