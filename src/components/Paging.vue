<template>
  <div class="paging">
    <button v-for="(page, idx) in totalPage" :key="idx" @click="movePage(page)">
      {{ page }}
    </button>
  </div>
</template>

<script>
export default {
  props: ["totalPage"],
  data() {
    return {};
  },
  methods: {
    movePage(page) {
      this.$emit("movePage", page);
    },
  },
};
</script>

<style>
.paging {
  position: absolute;
  bottom: -3rem;
}
</style>
