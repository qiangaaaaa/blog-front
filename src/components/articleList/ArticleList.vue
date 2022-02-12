<template>
  <div class="mainBox">
    <div class="listBox">
      <ul
        class="infinite-list"
        :router="true"
        v-loading="loading"
        element-loading-background="rgba(0, 0, 0, 0.6)"
      >
        <li
          class="infinite-list-item listBody"
          v-for="article in pageInfo.list"
        >
          <img :src="article.imageUrl" alt="" />
          <router-link
            :to="{ path: 'article/' + article.articleId }"
            tag="span"
          >
            <h1 v-html="article.title"></h1>
            <p>{{ article.articleIntroduction }}</p>
          </router-link>
        </li>
      </ul>
    </div>

    <div class="pageBox">
      <el-pagination
        v-if="totalCount / pageSize > 1"
        background
        layout="prev, pager, next"
        :total="totalCount"
        :page-size="pageSize"
        @current-change="currentChange"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      loading: false,
      pageInfo: null,
      currentPage: 1,
      totalCount: null,
      pageSize: 2,
    };
  },
  mounted() {
    this.getArticleList();
    // this.searchArticleListId = PubSub.subscribe(
    //   "searchArticleList",
    //   this.getSearchArticleList
    // );
    this.$bus.$on("searchArticleList", this.getSearchArticleList);
  },
  beforeDestroy() {
    // PubSub.unsubscribe(this.searchArticleListId);
    this.$bus.$off("searchArticleList");
  },
  methods: {
    // 接收搜索到的文章列表
    getSearchArticleList(data) {
      console.log("接收到搜索文章列表", data)
      this.pageInfo = data;
    },
    getArticleList() {
      this.getPageInfo(this.pageSize, this.currentPage);
    },
    currentChange(currentPage) {
      this.getPageInfo(this.pageSize, currentPage);
    },
    getPageInfo(pageSize, currentPage) {
      this.loading = true;
      let searchParam = {
        limit: pageSize,
        page: currentPage,
        key: "基础",
        categoryId: "",
        labelId: 9,
      };
      // console.log(searchParam)
      // axios.post("http://localhost:9000/blog/article/search", searchParam)
      axios
        .post("http://121.199.72.90:9000/blog/article/search", searchParam)
        .then((response) => {
          console.log(response);
          this.pageInfo = response.data.data;
          this.currentPage = this.pageInfo.currPage;
          this.totalCount = this.pageInfo.totalCount;
          this.pageSize = this.pageInfo.pageSize;
          this.loading = false;
          // console.log(this.pageInfo, this.currentPage, this.totalCount, this.pageSize)
        });
    },
  },
};
</script>

<style>
.mainBox {
  /*background-color: rgb(52, 50, 50);*/
  background-color: #353535;
  padding-bottom: 15px;
}

.listBox::-webkit-scrollbar {
  width: 0 !important;
}

.listBox {
  width: 100%;
  color: #d9d9d9;
  margin-bottom: 40px;
  padding-top: 30px;
  padding-bottom: 30px;
}

.pageBox {
  text-align: center;
}

.listBody {
  height: 180px;
  width: 90%;
  background-color: #353535;
  margin-top: 30px;
  margin-left: 5%;
  border-radius: 8px;
  box-shadow: #282828 0 0 10px;
  position: relative;
  transition: box-shadow 0.2s;
  border: 1px solid rgba(50, 50, 50, 0.4);
}

.listBody:hover {
  box-shadow: rgba(23, 22, 22, 1) 0 0 20px;
}

.listBody img {
  width: 30%;
  height: 100%;
}

.listBody span {
  position: absolute;
  display: block;
  left: 350px;
  top: 0;
}

/*修改element默认的颜色*/
.btn-prev,
.btn-next,
.number {
  background-color: #353535 !important;
  color: #d9d9d9 !important;
}

.active {
  background-color: #3c6e71 !important;
}

.el-icon {
  color: #d9d9d9 !important;
}
</style>
