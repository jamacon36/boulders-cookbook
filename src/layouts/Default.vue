<template>
  <div class="layout">
    <main class="page-content">
      <header class="hero">
        <g-image src="~/assets/home/home-hero.jpg" />
      </header>
      <slot />
    </main>
    <footer>
      <div class="container">
        <div class="grid">
          <div class="grid-1of1">
            The Boulders Cookbook
          </div>
          <div class="grid-1of3">
            The Boulders Cookbook
            <a href="mailto:fennmacon@gmail.com">fennmacon@gmail.com</a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>
