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
        <EquipeForm :formEquipe="formEquipe" @onFormSubmitEquipe="onFormSubmitEquipe"/>
        <EquipeList :equipes="equipes" @onDeleteEquipe="onDeleteEquipe" @onEditEquipe="onEditEquipe"/>
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
      formEquipe: {nom:"", isEdit:false}
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
    },
    onDeleteEquipe(id){
      axios.delete(this.urlEquipe+"/"+id).then(() => {
          this.getEquipes();
        })
        .catch(e => {
          alert(e);
        });
    },
    createEquipe(data) {
      axios.post(this.urlEquipe, {
          name: data.name
        })
        .then(() => {
          this.getEquipes();
        })
        .catch(e => {
          alert(e);
        });
    },
    editEquipe(data) {
      axios
        .put(this.urlEquipe+"/"+data.id, {
          name: data.name
        })
        .then(() => {
          this.getEquipes();
        })
        .catch(e => {
          alert(e);
        });
    },
    onEditEquipe(data) {
      this.formEquipe = data;
      this.formEquipe.isEdit = true;
    },
    onFormSubmitEquipe(data) {
      if (data.isEdit) {
        this.editEquipe(data);
      } else {
        this.createEquipe(data);
      }
    }
  },
  created() {
    this.getEquipes();
    this.getMatchs();
  }
}
</script>
