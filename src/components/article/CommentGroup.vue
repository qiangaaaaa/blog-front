<template>
  <div>
    <div class="commentGroup">
      <!--评论-->
      <div class="comment">
        <p>
          <span class="name-span">{{ comment.commentNickname }}</span>
        </p>
        <p class="content">{{ comment.content }}</p>
        <p class="content-info">
          <span class="timespan">{{ comment.commentTime }}</span>
          <span class="pointer replyspan" @click="openReply(comment.commentNickname)">回复</span>
        </p>
      </div>
      <!--回复-->
      <div class="reply">
        <div class="replyBody" v-for="reply in showReply">
          <p class="content">
            <span class="name-span">{{ reply.replyNickname }}</span>
            <span class="name-span" v-if="reply.parentReplyId != 0">回复 {{ reply.targetNickName }}：</span>
            <span>{{ reply.content }}</span>
          </p>
          <p>
            <span class="timespan">{{ reply.replyTime }}</span>
            <span class="pointer replyspan" @click="openReply(reply.replyNickname, reply.replyId)">回复</span>
          </p>
        </div>
        <p class="replystatistics" v-if="comment.replyResponseVOS.length > 2 && showTip">
          <span>共 {{ comment.replyResponseVOS.length }} 条回复</span>
          <span class="pointer" @click="showAllReply">查看全部</span>
        </p>

        <!-- 添加回复组件 -->
        <comment-and-reply-add v-if="replyShow"
          :receiveContent="defaultContent"
          :receiveType="'1'"
          :receiveCommentId="comment.commentId"
          :receiveParentReplyId="parentReplyId"
          :receiveArticleId="comment.articleId"
        />
      </div>
    </div>
    <el-divider></el-divider>
  </div>
</template>

<script>
import CommentAndReplyAdd from './CommentAndReplyAdd.vue';
export default {
  data() {
    return {
      replyShow: false,
      defaultContent:'',
      parentReplyId: '',
      showReply: this.comment.replyResponseVOS.slice(0, 2),
      showTip: true
    };
  },

  props: ["comment"],

  components: { CommentAndReplyAdd },

  computed: {},

  mounted: {},

  methods: {
    showAllReply() {
      this.showReply = this.comment.replyResponseVOS
      this.showTip = false;
    },
    openReply(nickName, parentReplyId) {
      this.parentReplyId = parentReplyId;
      this.replyShow = !this.replyShow
      this.defaultContent = 'to:' + nickName
    }
  },
};
</script>

<style>
.content-info span, .replystatistics span {
  font-size: 6px;
}

.name-span {
  color: #409eff;
}

.commentGroup::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
}

.content {
  margin-top: 8px;
  margin-bottom: 8px;
}

/* 回复相关的css */
.reply {
  float: right;
  width: 98%;
}

.replyBody {
  margin-bottom: 20px;
}

.replyspan {
  margin-left: 20px;
}

.replyspan:hover {
  color: #409eff;
}

/* 指针样式 */
.pointer {
  cursor: pointer;
}
</style>
