<template>
    <tr>
        <td>{{ equipe.id }}</td>
        <td>{{ equipe.nom }}</td>
        <td>
            <div class="buttons are-small is-centered">
                <button class="button is-success">Modifier</button>
                <button class="button is-danger">Supprimer</button>
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
  }
};
</script>