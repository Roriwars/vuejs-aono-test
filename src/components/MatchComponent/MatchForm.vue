<template>
    <div>
        <div class="columns is-desktop is-centered">
            <div class="column">
                <div class="field">
                    <label class="label">Equipe Locale</label>
                    <div class="control is-expanded">
                        <div class="select is-fullwidth">
                            <select id="selectLocale" v-model="formMatch.idEquipeLocale">
                                <option disabled value="" selected>Choisissez une équipe</option>
                                <option v-for="equipe in equipes" v-bind:key="equipe.id" v-bind:value="equipe.id">{{equipe.nom}}</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="field">
                    <label class="label">Equipe Visiteuse</label>
                    <div class="control is-expanded">
                        <div class="select is-fullwidth">
                            <select id="selectVisiteuse" v-model="formMatch.idEquipeVisiteuse">
                                <option disabled value="" selected>Choisissez une équipe</option>
                                <option v-for="equipe in equipes" v-bind:key="equipe.id" v-bind:value="equipe.id">{{equipe.nom}}</option>
                            </select>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="columns is-centered">
            <div class="field">
                <div class="control is-expanded has-text-centered">
                    <button class="button is-info" @click="onFormSubmitMatch">
                        {{btn}}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'MatchForm',
    data(){
        return{
            btn:"Ajouter",
        }
    },
    props:{
        formMatch: {
            type:Object
        },
        equipes: {
            type:Array
        }
    },
    methods: {
        onFormSubmitMatch(event) {
            event.preventDefault();
            if (this.formValidation()) {
                this.$emit("onFormSubmitMatch", this.formMatch);
                this.btn = "Ajouter";
                this.clearFormFields();
            }
        },
        formValidation() {
            if (document.getElementById("selectLocale").value === "" || document.getElementById("selectVisiteuse").value === "") {
                alert("Sélectionnez correctement les équipes");
                return false;
            }
            if (document.getElementById("selectVisiteuse").value === document.getElementById("selectLocale").value) {
                alert("Sélectionnez des équipes différentes");
                return false;
            }
            return true;
        },
        clearFormFields() {
            this.formMatch.idEquipeLocale = '';
            this.formMatch.idEquipeVisiteuse = '';
            this.formMatch.nomEquipeLocale = "";
            this.formMatch.nomEquipeVisiteuse = "";
            this.formMatch.isEdit = false;
            document.querySelector("#selectLocale").value="";
            document.querySelector("#selectVisiteuse").value="";
        }
    },
    updated() {
        if (this.formMatch.isEdit) {
            this.btn = "Modifier";
        }
    }
}
</script>