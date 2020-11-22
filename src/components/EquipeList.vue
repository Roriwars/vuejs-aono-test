<template>
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
            />
        </tbody>
    </table>
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
  }
};
</script>