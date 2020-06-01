<template>
  <Layout>
    <article class="recipe-list">
      <div class="container">
        <Breadcrumbs :breadcrumbs="breadcrumbTrail" />
        <h1>{{ header }}</h1>
        <ul>
          <li v-for="({ node }, index) of recipes" :key="index" class="recipe">
            <g-link :to="`/recipe/${node.slug}`">
              <p v-html="node.title" />
              <p class="author">by: {{ node.author.name }}</p>
            </g-link>
          </li>
        </ul>
      </div>
    </article>
  </Layout>
</template>

<page-query>
  query recipeCategories {
    allWordPressRecipe(sortBy: "title", order: ASC) {
      edges {
        node {
          title
          slug
          author {
            name
          }
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
@import "@/styles/pages/recipe-list.scss";
</style>

<script>
import Breadcrumbs from "@/components/Breadcrumbs.vue";

export default {
  name: "RecipeList",
  data() {
    return {
      recipes: [],
    };
  },
  computed: {
    header() {
      return this.$route.params.category.replace(/-/g, " ");
    },
    breadcrumbTrail() {
      return [
        { name: "Home", link: "/" },
        { name: this.header, link: `/recipes/${this.$route.params.category}` },
      ];
    },
  },
  components: {
    Breadcrumbs,
  },
  mounted() {
    this.recipes = this.$page.allWordPressRecipe.edges.filter(({ node }) =>
      node.categories.find(({ slug }) => slug === this.$route.params.category)
    );
  },
};
</script>
