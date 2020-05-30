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
          <li>
            <g-link to="/recipes/cocktails">Cocktails</g-link>
          </li>
          <li>
            <g-link to="/recipes/appetizers">Appetizers</g-link>
          </li>
          <li>
            <g-link to="/recipes/bread">Bread</g-link>
          </li>
          <li>
            <g-link to="/recipes/salad">Salad</g-link>
          </li>
          <li>
            <g-link to="/recipes/vegetables">Vegetables</g-link>
          </li>
          <li>
            <g-link to="/recipes/fish">Fish</g-link>
          </li>
          <li>
            <g-link to="/recipes/meat-poultry">Meat & Poultry</g-link>
          </li>
          <li>
            <g-link to="/recipes/pasta">Pasta</g-link>
          </li>
          <li>
            <g-link to="/recipes/dessert">Dessert</g-link>
          </li>
        </ul>
      </div>
    </article>
  </Layout>
</template>

<style lang="scss">
@import "@/styles/pages/home.scss";
</style>

<script>
export default {
  metaInfo: {
    title: "Home",
  },
};
</script>
