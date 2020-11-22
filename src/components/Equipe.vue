<template>
    <tr>
        <td>{{ equipe.id }}</td>
        <td>{{ equipe.nom }}</td>
        <td>
            <div class="buttons are-small is-centered">
                <button class="button is-success" @click="onEditEquipe">Modifier</button>
                <button class="button is-danger" @click="onDeleteEquipe">Supprimer</button>
            </div>
        </td>
    </tr>
</template>

<script>

export default {
    name: 'Equipe',
    props:{
        equipe: {
            type:Object
        }
    },
    methods: {
        onDeleteEquipe() {
            window.console.log("customer delete " + this.equipe.id);
            this.$emit("onDeleteEquipe", this.equipe.id);
        },
        onEditEquipe() {
            window.console.log("equipe edit " + this.equipe.id);
            this.$emit("onEditEquipe", this.equipe);
        }
    }
};
</script>