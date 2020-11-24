<template>
    <tr>
        <td>{{ match.id }}</td>
        <td>{{ match.nomEquipeLocale}}</td>
        <td>{{ match.nomEquipeVisiteuse}}</td>
        <td>
            <div class="buttons are-small is-centered">
                <button class="button is-success" @click="onEditMatch">Modifier</button>
                <button class="button is-danger" @click="onDeleteMatch">Supprimer</button>
            </div>
        </td>
    </tr>
</template>

<script>

export default {
  name: 'Match',
  props:{
        match: {
            type:Object
        }
  },
    methods: {
        onDeleteMatch() {
            console.log("match delete " + this.match.id);
            this.$emit("onDeleteMatch", this.match.id);
        },
        onEditMatch() {
            console.log("match edit " + this.match.id);
            this.$emit("onEditMatch", this.match);
        }
    }
};
</script>