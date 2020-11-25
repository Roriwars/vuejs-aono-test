<template>
    <div class="column">
        <table class="table is-fullwidth is-striped has-text-centered">
            <thead>
                <tr>
                <th>#</th>
                <th>Nom</th>
                <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <Equipe 
                    v-for="equipe in equipes"
                    :key="equipe.id"
                    :equipe="equipe"
                    @onDeleteEquipe="onDeleteEquipe"
                    @onEditEquipe="onEditEquipe"
                />
            </tbody>
        </table>
    </div>
</template>

<script>
import Equipe from "./Equipe"

export default {
  name: 'EquipeList',
  components: {
      Equipe
  },
  props:{
      equipes: {
          type:Array
      }
  },
  methods: {
    onDeleteEquipe(id) {
        this.$emit("onDeleteEquipe", id);
    },
    onEditEquipe(data) {
        this.$emit("onEditEquipe", data);
    }
  }
};
</script>