<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container"></div>
    </section>
  </div>
</template>

<script>
import search from "@/components/Search.vue";
import axios from "axios";
export default {
  components: { search },
  data() {
    return {
      search: "",
    };
  },
  methods: {},
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
