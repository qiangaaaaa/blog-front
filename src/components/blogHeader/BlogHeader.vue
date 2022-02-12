<template>
  <div class="imageBox">
    <img
      src="https://blog-lh.oss-cn-chengdu.aliyuncs.com/2021-12-22/8a16a90e8efdbf6ae75e3d29a29b4696.jpg"
      alt=""
    />
    <blog-search />
  </div>
</template>

<script>
import BlogSearch from "../blogSearch/BlogSearch.vue";
import RightNavBar from "../rightNavBar/RightNavBar.vue";

export default {
  components: { BlogSearch, RightNavBar },

  name: "BlogHeader",
  data() {
    return {};
  },
  methods: {
    //跳转到首页
    toHome() {
      window.location.href = "http://localhost:8080";
    },
  },
  mounted: {},
};
</script>

<style scoped>
.imageBox {
  height: 300px;
  overflow: hidden;
}
</style>
