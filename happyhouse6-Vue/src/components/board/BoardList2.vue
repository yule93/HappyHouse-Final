<template>
  <b-container class="bv-example-row mt-3">
    <b-row>
      <b-col>
        <h3>글목록</h3>
      </b-col>
    </b-row>
    <b-row class="mb-1">
      <b-col class="text-right">
        <b-button variant="primary" @click="moveWrite()">글쓰기</b-button>
      </b-col>
    </b-row>
    <b-row style="background-color: white; margin-top: 10px">
      <b-col>
        <b-table
          striped
          hover
          :items="articles"
          :fields="fields"
          @row-clicked="viewArticle"
        >
        </b-table>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { listArticle } from "@/api/board";

export default {
  name: "BoardList",
  components: {},
  data() {
    return {
      articles: [],
      fields: [
        {
          key: "articleno",
          label: "글번호",
          tdClass: "tdClass",
          sortable: true,
        },
        { key: "subject", label: "제목", tdClass: "tdSubject" },
        { key: "userid", label: "작성자", tdClass: "tdClass" },
        { key: "regtime", label: "작성일", tdClass: "tdClass", sortable: true },
        { key: "hit", label: "조회수", tdClass: "tdClass" },
      ],
    };
  },
  created() {
    let param = {
      pg: 1,
      spp: 20,
      key: null,
      word: null,
    };
    listArticle(
      param,
      (response) => {
        this.articles = response.data;
      },
      (error) => {
        console.log(error);
      }
    );
  },
  methods: {
    moveWrite() {
      this.$router.push({ name: "BoardWrite" });
    },
    viewArticle(article) {
      this.$router.push({
        name: "BoardView",
        params: { articleno: article.articleno },
      });
    },
  },
};
</script>

<style scope>
.tdClass {
  width: 50px;
  text-align: center;
}
.tdSubject {
  width: 300px;
  text-align: left;
}
</style>
