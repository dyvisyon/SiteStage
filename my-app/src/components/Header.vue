<template>
<header>
  <div>
  <b-navbar class="shadow mb-5" toggleable="xl" type="dark">
    <b-navbar-brand href="/">HOTEL DE BRIERE</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item-dropdown text="L'association" right>
          <b-dropdown-item href="#">Présentation</b-dropdown-item>
          <b-dropdown-item href="#">Son histoire</b-dropdown-item>
          <b-dropdown-item href="#">Nous joindre</b-dropdown-item>
          <b-dropdown-item href="#">Partenaires</b-dropdown-item>
        </b-nav-item-dropdown>
        <b-nav-item-dropdown text="Le projet" right>
          <b-dropdown-item href="#">L'emergence</b-dropdown-item>
          <b-dropdown-item href="#">La convention</b-dropdown-item>
        </b-nav-item-dropdown>
        <b-nav-item href="#">La phase d'amorçage</b-nav-item>
        <b-nav-item href="#">Le chantier</b-nav-item>
        <b-nav-item href="#">Evenements</b-nav-item>
        <b-nav-item href="articles">On en parle</b-nav-item>
        <b-nav-item href="#">Ressources</b-nav-item>
        <b-nav-item href="admin">Administration</b-nav-item>
        

      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        


        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template v-slot:button-content>
            <em>Espace Perso</em>
          </template>
          <b-dropdown-item v-if="isConnected" href="profil">Profil</b-dropdown-item>
          <b-dropdown-item v-if="!isConnected" href="inscriptionConnexion">Se connecter</b-dropdown-item>
          <b-dropdown-item v-on:click="signOutUser" href="/">Déconnexion</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</header>
</template>


<script>
import firebase from "firebase"
export default{
  data(){
    return{
      isConnected: false,
      user:''
    }
  },
  /*computed: { 
    get: function(){
      console.log("hello")
      this.user = firebase.auth().currentUser;
      if(this.user != null){
        this.isConnected = true;
      }
    }
  },*/
  created(){
    this.user = firebase.auth().currentUser;
    console.log(this.user)
    if(this.user != null){
      return this.isConnected = true;
    }
  },
  methods:{
    signOutUser(){
      firebase.auth().signOut().then(function() {
        alert("Vous êtes déconnecté. A bientôt");
      }).catch(function(error) {
        console.log(error.message)
        alert("Une erreur s'est produite. Vous n'êtes pas déconnecté.");
    });
    }
  }
}
</script>

<style>
.headersize{
  width: auto;
  height: 500px;
  background-image: url('../assets/img/fondSite.jpg');
}

</style>