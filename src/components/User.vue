<template>
  <div class="layout">
    <div v-for="(user, idx) in users" :key="idx">
      <h2>{{ user.first_name }}</h2>
      <img :src="`${user.avatar}`" alt />
    </div>
    <Paging :totalPage="totalPage" @movePage="movePage" />
  </div>
</template>

<script>
import axios from "axios";
import Paging from "@/components/Paging";

export default {
  components: {
    Paging,
  },
  data() {
    return {
      users: null,
      totalPage: null,
      pageNum: 1,
    };
  },
  methods: {
    fetchData(pageNum) {
      axios
        .get("https://reqres.in/api/users?page=" + pageNum)
        .then((res) => {
          this.users = res.data.data;
          this.totalPage = res.data.total_pages;
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    movePage(page) {
      this.fetchData(page);
    },
  },
  created() {
    this.fetchData(this.pageNum);
  },
};
</script>

<style>
.layout {
  position: relative;
  display: flex;
  justify-content: space-evenly;
}
</style>
