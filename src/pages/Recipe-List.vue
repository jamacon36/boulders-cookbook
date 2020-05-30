<template>
  <Layout>
    <article class="recipe-list">
      <div class="container">
        <h1>{{ header }}</h1>
      </div>
    </article>
  </Layout>
</template>

<style lang="scss">
@import "@/styles/pages/recipe-list.scss";
</style>

<script>
export default {
  name: "RecipeList",
  computed: {
    header() {
      return this.$route.params.category.replace(/-/g, " ");
    }
  }
};
</script>
