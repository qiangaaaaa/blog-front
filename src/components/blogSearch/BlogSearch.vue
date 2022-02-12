<template>
  <div class="searchBox">
    <input
      class="searchInput"
      type="text"
      placeholder="search..."
      v-model="searchKey"
      @keyup.enter="search"
    />
    <div class="searchIcon el-icon-search" @click="search"></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      searchKey: "",
    };
  },
  methods: {
    search() {
      let searchParam = {
        limit: 10,
        page: 1,
        key: this.searchKey,
      };
      axios
        .post("http://121.199.72.90:9000/blog/article/search", searchParam)
        .then((response) => {
          // PubSub.publish("searchArticleList", response.data.data)
          this.$bus.$emit("searchArticleList", response.data.data); //发送数据
        });
    },
  },
};
</script>


    
<style>
.searchBox {
  position: absolute;
  top: 200px;
  left: 35%;
  width: 500px;
  height: 60px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  background-color: rgba(255, 255, 255, 0.3);
  transition: all 0.3s ease-out;
}
.searchBox:hover,
.searchBox:checked {
  box-shadow: rgba(255, 255, 255, 0.8) 0 0 4px;
  background-color: rgba(255, 255, 255, 0.8);
}

.searchInput {
  display: block;
  width: 430px;
  height: 100%;
  padding: 20px;
  border-bottom-left-radius: 30px;
  border-top-left-radius: 30px;
  font-size: 18px;
  background-color: rgba(0, 0, 0, 0);
  color: #444444;
}

.searchIcon {
  position: absolute;
  width: 60px;
  height: 60px;
  top: 0;
  right: 0;
}

.el-icon-search {
  color: rgb(139, 139, 139);
  font-size: 30px;
  line-height: 60px;
  border-bottom-right-radius: 30px !important;
  border-top-right-radius: 30px !important;
  text-align: center;
}
</style>