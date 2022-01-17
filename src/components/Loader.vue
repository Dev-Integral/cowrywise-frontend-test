<template>
    <ContentLoader
    viewBox="0 0 450 400"
    backgroundColor="#f0f0f0"
    foregroundColor="#dedede"
  >
    <rect x="43" y="304" rx="4" ry="4" width="271" height="20" />
    <rect x="44" y="333" rx="4" ry="4" width="200" height="9" />
    <rect x="42" y="-170" rx="10" ry="10" width="400" height="407" />
  </ContentLoader>
</template>

<script>
import { ContentLoader } from "vue-content-loader";
export default {
  name: "Loader",
  components: { ContentLoader },
};
</script>

<style lang="scss" scoped>
h2 {
  font-size: 30px;
  color: black;
}
</style>