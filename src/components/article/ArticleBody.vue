<template>
  <div class="articleBody" v-html="articleContent"></div>
</template>

<script>
export default {
  data() {
    return {
      articleContent: this.articleBody,
    };
  },
  props: ["articleBody"],
  methods: {},
};
</script>