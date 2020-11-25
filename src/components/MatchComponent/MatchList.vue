<template>
    <div class="column">
    <table class="table is-fullwidth is-striped has-text-centered">
        <thead>
            <tr>
                <th>#</th>
                <th>Equipe locale</th>
                <th>Equipe visiteuse</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <Match 
                v-for="match in matchs"
                :key="match.id"
                :match="match"
                @onDeleteMatch="onDeleteMatch"
                @onEditMatch="onEditMatch"
            />
        </tbody>
    </table>
    </div>
</template>

<script>
import Match from "./Match"

export default {
  name: 'MatchList',
  components: {
      Match
  },
  props:{
      matchs: {
          type:Array
      }
  },
  methods: {
    onDeleteMatch(id) {
        this.$emit("onDeleteMatch", id);
    },
    onEditMatch(data) {
        this.$emit("onEditMatch", data);
    }
  }
};
</script>