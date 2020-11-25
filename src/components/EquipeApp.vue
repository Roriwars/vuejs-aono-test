<template>
    <div class="column">
        <div class="title has-text-centered">Les équipes</div>
        <EquipeForm :formEquipe="formEquipe" @onFormSubmitEquipe="onFormSubmitEquipe"/>
        <Loader v-if="loader"/>       
        <EquipeList v-if="!loader" :equipes="equipes" @onDeleteEquipe="onDeleteEquipe" @onEditEquipe="onEditEquipe"/>
    </div>
</template>

<script>
import axios from "axios";
import EquipeForm from "./EquipeComponent/EquipeForm";
import EquipeList from "./EquipeComponent/EquipeList";
import Loader from "./Loader"

export default {
  name: 'EquipeApp',
  components:{
    EquipeForm,
    EquipeList,
    Loader
  },
  data() {
    return {
      urlEquipe: "http://api-laravel-aono.test/api/equipes",
      equipes: [],
      formEquipe: {nom:"", isEdit:false},
      loader:false
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
    onDeleteEquipe(id){
      this.loader=true;
      axios.delete(this.urlEquipe+"/"+id).then(() => {
          this.getEquipes();
        })
        .catch(e => {
          alert(e);
        });
    },
    createEquipe(data) {
      this.loader=true;
      axios.post(this.urlEquipe, {
          nom: data.nom
        })
        .then(() => {
          this.getEquipes();
        })
        .catch(e => {
          alert(e);
        });
    },
    editEquipe(data) {
      this.loader=true;
      axios
        .put(this.urlEquipe+"/"+data.id, {
          nom: data.nom
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
  }
}
</script>
