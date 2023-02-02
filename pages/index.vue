<template>
  <div class="container">
    <Fromlogin />
    <p>{{ username }}</p>
    <p>{{ password }}</p>
    <p>{{ email }}</p>
  </div>
</template>

<script>
import Fromlogin from "../components/login/fromlogin.vue";
export default {
  data() {
    return {};
  },
  components: {
    Fromlogin,
  },
};
</script>

<style lang="scss" scoped></style>
