<template>
  <Layout>
    <article class="home-content">
      <div class="container">
        <h1>The Boulders Cookbook</h1>
        <p>
          Welcome to the renowned Boulders Cookbook! Click on a recepie category
          below to begin.
        </p>
        <ul>
          <li
            v-for="({ title, slug, count }, index) of categories"
            :key="index"
          >
            <g-link :to="`/recipes/${slug}`">{{ title }}</g-link>
          </li>
        </ul>
      </div>
    </article>
  </Layout>
</template>

<page-query>
  query recipeCategories {
    allWordPressRecipe {
      edges {
        node {
          title
          slug
          categories {
            title
            slug
            count
          }
        }
      }
    }
  }
</page-query>

<style lang="scss">
@import "@/styles/pages/home.scss";
</style>

<script>
export default {
  name: "Home",
  metaInfo: {
    title: "Home",
  },
  data() {
    return {
      categories: [],
    };
  },
  mounted() {
    const recipeCategories = this.$page.allWordPressRecipe.edges.map(
      ({ node }) => node.categories
    );
    recipeCategories.forEach((categories) => {
      categories.forEach(({ title, slug, count }) => {
        if (
          !this.categories.find(({ slug: addedSlug }) => addedSlug === slug)
        ) {
          this.categories.push({ title, slug, count });
        }
      });
    });
  },
};
</script>
