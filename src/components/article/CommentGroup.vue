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
      <div class="replyBody" v-for="reply in comment.replyResponseVOS.slice(0,2)">
        <span>{{ reply.replyNickname }}</span>
        <span v-if="reply.parentReplyId != 0">
          回复 {{ reply.targetNickName }}：</span
        >
        <span>{{ reply.content }}</span>
        <p>
          <span class="timespan">{{ reply.replyTime }}</span>
          <span class="pointer replyspan">回复</span>
        </p>
      </div>
      <p class="replystatistics" v-if="comment.replyResponseVOS.length > 2"><span>共 {{comment.replyResponseVOS.length}} 条回复</span> <span class="pointer">查看全部</span> </p>
      <div class="replyadd">

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

.commentGroup::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
}

/* 回复相关的css */
.reply {
  float: right;
  width: 98%;
}

.replyBody {
  margin-bottom: 12px;
}

.replyspan:hover {
  color: #409EFF
}

/* 指针样式 */
.pointer {
  cursor: pointer;
}
</style>