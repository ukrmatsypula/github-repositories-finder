<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <!-- erorrs -->
        <div class="errors" v-if="error">
          <p>{{ this.error }}</p>
        </div>

        <Search
          :value="search"
          placeholder="Type username..."
          @search="search = $event"
        />

        <button v-if="!repos" class="btn btnPrimary" @click="getRepos">
          Search
        </button>
        <button v-else class="btn btnPrimary" @click="getRepos">
          Search Again
        </button>

        <div class="repos__wrapper" v-if="repos">
          <div class="repo-item" v-for="repo in repos" :key="repo.id">
            <div class="repos-info">
              <a class="link" :href="repo.html_url" target="_blank">{{
                repo.name
              }}</a>
              <span>{{ repo.stargazers_count }}⭐</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Search from "@/components/Search.vue";
export default {
  components: { Search },
  data() {
    return {
      search: "",
      repos: null,
      error: null,
    };
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((response) => {
          this.error = null;
          this.repos = response.data;
        })
        .catch((error) => {
          console.log(error);
          this.repos = null;
          this.error = "Can't find this user";
        });
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

.errors {
  margin-bottom: 20px;
}
</style>
