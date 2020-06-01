<template>
  <Layout>
    <article class="recipe">
      <div class="container">
        <Breadcrumbs :breadcrumbs="breadcrumbTrail" />
        <header>
          <h1 v-html="recipe.title" />
          <p>By: {{ recipe.author.name }}</p>
        </header>
        <section class="recipe__equipment">
          <div class="ingredients">
            <h2>Ingredients</h2>
            <ul>
              <li
                v-for="({ name, qty, notes }, index) of recipe.acf.ingredients"
                :key="index"
                class="ingredients__ingredient"
              >
                {{ name }} - {{ qty }} {{ notes ? `(${notes})` : "" }}
              </li>
            </ul>
          </div>
          <div class="info">
            <h2>Recipe Info</h2>
            <ul>
              <li v-if="prepTime" class="info__prep">
                Prep Time: {{ prepTime }}
              </li>
              <li v-if="cookTime" class="info__cook">
                Cook Time: {{ cookTime }}
              </li>
              <li v-if="recipe.acf.recipeInfo.yield" class="info__yield">
                Yields: {{ recipe.acf.recipeInfo.yield }}
              </li>
              <li v-if="recipe.acf.recipeInfo.servings" class="info__servings">
                Serves: {{ recipe.acf.recipeInfo.servings }}
              </li>
            </ul>
          </div>
          <div v-if="recipe.acf.tools.length" class="tools">
            <h2>Tools</h2>
            <ul>
              <li
                v-for="({ tool }, index) of recipe.acf.tools"
                :key="index"
                class="tools__tool"
              >
                {{ tool }}
              </li>
            </ul>
          </div>
        </section>
        <section>
          <div class="directions">
            <h2>Directions</h2>
            <div class="directions__content" v-html="recipe.acf.directions" />
          </div>
          <div v-if="recipe.acf.notes" class="notes">
            <h2>Notes</h2>
            <div class="directions__notes" v-html="recipe.acf.notes" />
          </div>
        </section>
      </div>
    </article>
  </Layout>
</template>

<page-query>
query Recipe ($path: String!) {
  wordPressRecipe (path: $path) {
    title
    slug
    author {
      name
    }
    acf {
      ingredients {
        name
        qty
        notes
      }
      recipeInfo {
        prepTime
        cookTime
        yield
        servings
      }
      tools {
        tool
      }
      directions
      notes
    }
    categories {
      title
      slug
      id
    }
  }
}
</page-query>

<style lang="scss">
@import "@/styles/templates/recipe.scss";
</style>

<script>
import Breadcrumbs from "@/components/Breadcrumbs.vue";

export default {
  name: "RecipePost",
  data() {
    return {
      recipe: {},
    };
  },
  computed: {
    prepTime() {
      if (!this.recipe.acf.recipeInfo.prepTime) return null;
      return this.makeTime(this.recipe.acf.recipeInfo.prepTime);
    },
    cookTime() {
      if (!this.recipe.acf.recipeInfo.cookTime) return null;
      return this.makeTime(this.recipe.acf.recipeInfo.cookTime);
    },
    breadcrumbTrail() {
      const [{ title, slug }] = this.recipe.categories;
      return [
        { name: "Home", link: "/" },
        { name: title, link: `/recipes/${slug}` },
        { name: this.recipe.title, link: `/recipe/${this.recipe.slug}` },
      ];
    },
  },
  components: {
    Breadcrumbs,
  },
  methods: {
    makeTime(minString) {
      const mins = parseInt(minString, 10);
      return mins >= 60 ? `${mins / 60} hour(s)` : `${mins} min`;
    },
  },
  created() {
    this.recipe = this.$page.wordPressRecipe;
  },
};
</script>
