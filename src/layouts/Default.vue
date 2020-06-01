<template>
  <div class="layout">
    <main class="page-content">
      <header class="hero">
        <g-image src="~/assets/home/home-hero.jpg" />
      </header>
      <slot />
    </main>
    <footer class="site-footer">
      <div class="container">
        <div class="footer-title">
          The Boulders Cookbook
        </div>
        <div class="footer-contact">
          By:
          <a href="mailto:fennmacon@gmail.com">fennmacon@gmail.com</a>
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
