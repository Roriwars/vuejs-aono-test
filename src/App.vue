<template>
  <div id="app">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://www.aono.fr/">
          <img src="./assets/AONO.jpg" alt="aono.fr">
        </a>
      </div>
    </nav>
    <div class="container">
      <div class="column">
        <div class="title has-text-centered">Les équipes</div>
        <EquipeForm />
        <EquipeList :equipes="equipes"/>
      </div>
      <div class="column">
        <div class="title has-text-centered">Les matchs</div>
        <MatchForm />        
        <MatchList :matchs="matchs"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import EquipeForm from "./components/EquipeForm"
import EquipeList from "./components/EquipeList"
import MatchForm from "./components/MatchForm"
import MatchList from "./components/MatchList"

export default {
  name: 'App',
  components:{
    EquipeForm,
    EquipeList,
    MatchForm,
    MatchList
  },
  data() {
    return {
      urlEquipe: "http://api-aono-test.test/api/equipes",
      urlMatch: "http://api-aono-test.test/api/matchs",
      equipes: [],
      matchs:[],
    };
  },
  methods: {
    getEquipes() {
      axios.get(this.urlEquipe).then(data => {
        this.equipes = data.data;
        console.log(this.equipes);
        this.loader = false;
      });
    },
    getMatchs() {
      axios.get(this.urlMatch).then(data => {
        this.matchs = data.data;
        console.log(this.matchs);
        this.loader = false;
      });
    }
  },
  created() {
    this.getEquipes();
    this.getMatchs();
  }
}
</script>
