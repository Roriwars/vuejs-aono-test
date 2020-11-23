<template>
  <div id="app">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://www.aono.fr/">
          <img src="./assets/AONO.jpg" alt="aono.fr">
        </a>
      </div>
      <div class="navbar-menu">
        <a class="navbar-item">
          <router-link to="/" class="nav-link">Equipes</router-link>
        </a>
        <a class="navbar-item">
          <router-link to="/matchs" class="nav-link">Matchs</router-link>
        </a>
      </div>
    </nav>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>
