<template>
    <tr>
        <td>{{ match.id }}</td>
        <td>{{ match.nomEquipeLocale}}</td>
        <td>{{ match.nomEquipeVisiteuse}}</td>
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
  name: 'Match',
  props:{
      match: {
          type:Object
      }
  }
};
</script>