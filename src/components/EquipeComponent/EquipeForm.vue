<template>
    <div class="field is-grouped">
        <p class="control is-expanded">
            <input class="input" name="nom" type="text" :value="formEquipe.nom" @change="handleChange" placeholder="Nom de l'équipe">
        </p>
        <p class="control">
            <button class="button is-info" @click="onFormSubmitEquipe">
              {{btn}}
            </button>
        </p>
    </div>
</template>

<script>

export default {
    name: 'EquipeForm',
    data(){
        return{
            btn:"Ajouter"
        }
    },
    props:{
        formEquipe: {
            type:Object
        }
    },
    methods: {
        handleChange(event) {
            const { name, value } = event.target;
            let formEquipe = this.formEquipe;
            formEquipe[name] = value;
            this.formEquipe = formEquipe;
        },
        onFormSubmitEquipe(event) {
            event.preventDefault();
            if (this.formValidation()) {
                this.$emit("onFormSubmitEquipe", this.formEquipe);
                this.btn = "Ajouter";
                this.clearFormFields();
            }
        },
        formValidation() {
            if (document.getElementsByName("nom")[0].value === "") {
                alert("Entrez un nom pour l'équipe");
                return false;
            }
            return true;
        },
        clearFormFields() {
            this.formEquipe.nom = "";
            this.formEquipe.isEdit = false;
            document.querySelector(".input").value="";
        }
    },
    updated() {
        if (this.formEquipe.isEdit) {
            this.btn = "Modifier";
            document.querySelector(".input").value=this.formEquipe.nom;
        }
    }
}
</script>