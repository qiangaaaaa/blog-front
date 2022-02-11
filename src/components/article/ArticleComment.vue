<template>
    <div class="commentInfo">
      <div class="commentBody" v-for="comment in comments">
        <!--评论-->
        <div class="comment">
          <span>{{ comment.commentNickname }}</span>
          <span>{{ comment.commentTime }}</span>
          <p class="comment">{{ comment.content }}</p>
          <!--回复-->
          <div class="replyBody" v-for="reply in comment.replyResponseVOS">
            <span>{{ reply.replyNickname }}</span>
            <span v-if="reply.parentReplyId != 0">
              回复 {{ reply.targetNickName }}</span
            >
            <br />
            <span>{{ reply.content }}</span>
            <p>{{ reply.replyTime }}</p>
          </div>
        </div>
      </div>
      </div>
    </div>
</template>

<script>
export default {
     props:['commnets']
}
</script>