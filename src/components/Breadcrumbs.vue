<template>
  <div class="breadcrumbs">
    <ul class="menu breadcrumbs__menu">
      <li
        v-for="({ name, link }, index) of breadcrumbs"
        :key="index"
        class="breadcrumb"
      >
        <g-link :to="link">
          <span v-html="name" />
        </g-link>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
@import "@/styles/components/breadcrumbs.scss";
</style>

<script>
export default {
  name: "Breadcrumbs",
  props: {
    breadcrumbs: Array,
  },
};
</script>
