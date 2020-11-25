<template>
    <div class="column">
        <div class="title has-text-centered">Les matchs</div>
        <MatchForm :formMatch="formMatch" :equipes="equipes" @onFormSubmitMatch="onFormSubmitMatch"/> 
        <Loader v-if="loader"/>       
        <MatchList v-if="!loader" :matchs="matchs" @onDeleteMatch="onDeleteMatch" @onEditMatch="onEditMatch"/>
    </div>
</template>

<script>
import axios from "axios";
import MatchForm from "./MatchComponent/MatchForm"
import MatchList from "./MatchComponent/MatchList"
import Loader from "./Loader"

export default {
  name: 'MatchApp',
  components:{
    MatchForm,
    MatchList,
    Loader
  },
  data() {
    return {
      urlEquipe: "http://api-laravel-aono.test/api/equipes",
      urlMatch: "http://api-laravel-aono.test/api/matchs",
      equipes: [],
      matchs:[],
      loader:false,
      formMatch: {idEquipeLocale:'', idEquipeVisiteuse:'', nomEquipeLocale:"", nomEquipeVisiteuse:"", isEdit:false}
    };
  },
  methods: {
    getEquipes() {
      this.loader=true;
      axios.get(this.urlEquipe).then(data => {
        this.equipes = data.data;
        this.loader=false;
      });
    },
    getMatchs() {
      this.loader=true;
      axios.get(this.urlMatch).then(data => {
        this.matchs = data.data;
        this.loader=false;
      });
    },
    onDeleteMatch(id){
      this.loader=true;
      axios.delete(this.urlMatch+"/"+id).then(() => {
          this.getMatchs();
        })
        .catch(e => {
          alert(e);
        });
    },
    createMatch(data) {
      axios.post(this.urlMatch, {
          idEquipeLocale: data.idEquipeLocale,
          idEquipeVisiteuse: data.idEquipeVisiteuse
        })
        .then(() => {
          this.getMatchs();
        })
        .catch(e => {
          alert(e);
        });
    },
    editMatch(data) {
      axios
        .put(this.urlMatch+"/"+data.id, {
          idEquipeLocale: data.idEquipeLocale,
          idEquipeVisiteuse: data.idEquipeVisiteuse
        })
        .then(() => {
          this.getMatchs();
        })
        .catch(e => {
          alert(e);
        });
    },
    onEditMatch(data) {
        this.formMatch = data;
        this.formMatch.isEdit = true;
    },
    onFormSubmitMatch(data) {
      this.loader=true;
        if (data.isEdit) {
            this.editMatch(data);
        } else {
            this.createMatch(data);
        }
    }
  },
  created() {
    this.getEquipes();
    this.getMatchs();
  }
}
</script>
