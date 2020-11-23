<template>
    <div class="column">
        <div class="title has-text-centered">Les équipes</div>
        <EquipeForm :formEquipe="formEquipe" @onFormSubmitEquipe="onFormSubmitEquipe"/>
        <EquipeList :equipes="equipes" @onDeleteEquipe="onDeleteEquipe" @onEditEquipe="onEditEquipe"/>
    </div>
</template>

<script>
import axios from "axios";
import EquipeForm from "./EquipeComponent/EquipeForm";
import EquipeList from "./EquipeComponent/EquipeList";

export default {
  name: 'EquipeApp',
  components:{
    EquipeForm,
    EquipeList,
  },
  data() {
    return {
      urlEquipe: "http://api-aono-test.test/api/equipes",
      urlMatch: "http://api-aono-test.test/api/matchs",
      equipes: [],
      formEquipe: {nom:"", isEdit:false},
    };
  },
  methods: {
    getEquipes() {
      axios.get(this.urlEquipe).then(data => {
        this.equipes = data.data;
        console.log(this.equipes);
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
        console.log("onEditEquipe");
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
