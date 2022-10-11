<template>
  <div class="row">
    <div
      class="card"
      v-show="info.users.length"
      v-for="user in info.users"
      :key="user.login"
    >
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <h1 v-show="info.isFirst">欢迎使用</h1>
    <h1 v-show="info.isLoading">加载中...</h1>
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: "ALlList",
  data() {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: "",
        users: [],
      },
    };
  },
  mounted() {
    this.$bus.$on("updateLisData", (dataObj) => {
      console.log("我是list组件，收到数据：", dataObj);
      this.info = { ...this.info, ...dataObj };
    });
  },
};
</script>

<style scoped>
</style>
