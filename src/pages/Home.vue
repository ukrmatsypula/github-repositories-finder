<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <!-- erorrs -->
        <Search
          :value="search"
          placeholder="Type username..."
          @search="search = $event"
        />

        <button class="btn btnPrimary" @click="getRepos">Search</button>
      </div>
    </section>
  </div>
</template>

<script>
import search from "@/components/Search.vue";
import axios from "axios";
import Search from "@/components/Search.vue";
export default {
  components: { Search },
  data() {
    return {
      search: "",
    };
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((response) => console.log(response))
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  align-items: center;
  flex-direction: column;
}
button {
  margin-top: 40px;
}
.repos__wrapper {
  width: 400px;
  margin: 30px 0;
}
.repos-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #dbdbdb;
}
</style>
