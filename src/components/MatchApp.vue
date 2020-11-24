<template>
    <div class="column">
        <div class="title has-text-centered">Les matchs</div>
        <MatchForm :formMatch="formMatch" :equipes="equipes" @onFormSubmitMatch="onFormSubmitMatch"/>        
        <MatchList :matchs="matchs" @onDeleteMatch="onDeleteMatch" @onEditMatch="onEditMatch"/>
    </div>
</template>

<script>
import axios from "axios";
import MatchForm from "./MatchComponent/MatchForm"
import MatchList from "./MatchComponent/MatchList"

export default {
  name: 'MatchApp',
  components:{
    MatchForm,
    MatchList
  },
  data() {
    return {
      urlEquipe: "http://api-laravel-aono.test/api/equipes",
      urlMatch: "http://api-laravel-aono.test/api/matchs",
      equipes: [],
      matchs:[],
      formMatch: {idEquipeLocale:null, idEquipeVisiteuse:null, nomEquipeLocale:"", nomEquipeVisiteuse:"", isEdit:false}
    };
  },
  methods: {
    getEquipes() {
      axios.get(this.urlEquipe).then(data => {
        this.equipes = data.data;
        console.log(this.equipes);
      });
    },
    getMatchs() {
      axios.get(this.urlMatch).then(data => {
        this.matchs = data.data;
        console.log(this.matchs);
      });
    },
    onDeleteMatch(id){
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
        console.log("onEditMatch");
        console.log(this.formMatch);
        console.log(data);
        this.formMatch = data;
        console.log(this.formMatch);
        this.formMatch.isEdit = true;
    },
    onFormSubmitMatch(data) {
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
