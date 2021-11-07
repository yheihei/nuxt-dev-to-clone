<template>
  <div class="default">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
      <div class="container">
        <nuxt-link to="/" class="navbar-brand">Dev</nuxt-link>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <nuxt-link to="/" class="nav-link">New</nuxt-link>
            </li>
            <li class="nav-item active">
              <nuxt-link to="/top" class="nav-link">Top</nuxt-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <nuxt keep-alive />
  </div>
</template>

<style>
.default {
  padding-top: 5rem;
}
</style>
