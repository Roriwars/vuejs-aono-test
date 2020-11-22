<template>
  <div id="app">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://www.aono.fr/">
          <img src="./assets/AONO.jpg" alt="aono.fr">
        </a>
      </div>
    </nav>
    <div class="container">
      <div class="column">
        <div class="title has-text-centered">Les équipes</div>
        <div class="field is-grouped">
          <p class="control is-expanded">
            <input class="input" type="text" placeholder="Nom de l'équipe">
          </p>
          <p class="control">
            <button class="button is-info">
              Ajouter
            </button>
          </p>
        </div>
        <table class="table is-fullwidth is-striped has-text-centered">
          <thead>
            <tr>
              <th>Id</th>
              <th>Nom</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1</td>
              <td>nomequipe</td>
              <td>
                <div class="buttons are-small is-centered">
                  <button class="button is-success">Modifier</button>
                  <button class="button is-danger">Supprimer</button>
                </div>
              </td>
            </tr>
            <tr>
              <td>2</td>
              <td>nomequipe2</td>
              <td>
                <div class="buttons are-small is-centered">
                  <button class="button is-success">Modifier</button>
                  <button class="button is-danger">Supprimer</button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="column">
        <div class="title has-text-centered">Les matchs</div>
        
        <div class="field is-horizontal">
          <div class="field-body">
            <div class="field">
              <label class="label">Equipe Locale</label>
              <div class="control is-expanded">
                <div class="select">
                  <select>
                    <option>Select dropdown</option>
                    <option>With options</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="field">
              <label class="label">Equipe Visiteuse</label>
              <div class="control is-expanded">
                <div class="select">
                  <select>
                    <option>Select dropdown</option>
                    <option>With options</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="field">
              <div class="control is-expanded has-text-centered">
                <button class="button is-info">
                  Ajouter
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <table class="table is-fullwidth is-striped has-text-centered">
          <thead>
            <tr>
              <th>Id</th>
              <th>Equipe locale</th>
              <th>Equipe visiteuse</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1</td>
              <td>nomequipe</td>
              <td>nomequipevisiteuse</td>
              <td>
                <div class="buttons are-small is-centered">
                  <button class="button is-success">Modifier</button>
                  <button class="button is-danger">Supprimer</button>
                </div>
              </td>
            </tr>
            <tr>
              <td>2</td>
              <td>nomequipe2</td>
              <td>nomequipevisiteuse2</td>
              <td>
                <div class="buttons are-small is-centered">
                  <button class="button is-success">Modifier</button>
                  <button class="button is-danger">Supprimer</button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  }
}
</script>

<style scoped>
  .is-vcentered{
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
  }
</style>
