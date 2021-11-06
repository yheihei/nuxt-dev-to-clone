<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light fixed-top">
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
    </nav>
    <nuxt keep-alive />
  </div>
</template>
