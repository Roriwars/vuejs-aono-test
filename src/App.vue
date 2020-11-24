<template>
  <div id="app">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://www.aono.fr/">
          <img src="./assets/AONO.jpg" alt="aono.fr">
        </a>

        <a class="navbar-burger" @click="navbarToggle">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>
      <div id="navbar" class="navbar-menu">
        <div class="navbar-start">
          <router-link to="/" class="navbar-item">Equipes</router-link>
          <router-link to="/matchs" class="navbar-item">Matchs</router-link>
        </div>
      </div>  
    </nav>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  methods:{
    navbarToggle(){
      document.getElementById("navbar").classList.toggle('is-active');
    }
  }
}
</script>
