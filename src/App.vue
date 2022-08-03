<template>
  <div id="app">
    <div v-if="isLoggedIn === true" class="header">
      <img :src="this.authUser.avatar">
      Logged in as : <strong>{{this.authUser.username}}</strong>
      <button v-on:click="logout">Logout</button>
    </div>
    <Login v-if="isLoggedIn === false" v-on:loggedIn="loggedIn"/>
    <NoteAdd v-if="isLoggedIn === true" v-on:noteAdded="noteAdded" v-bind:authUser="authUser"  />
    <NoteList v-if="isLoggedIn === true" :notes="this.notes" v-bind:authUser="authUser"  />
  </div>
</template>

<script>
import Login from './components/Login.vue'
import NoteAdd from './components/NoteAdd.vue'
import NoteList from './components/NoteList.vue'

export default {
  name: 'App',
  components: {
    Login,
    NoteAdd,
    NoteList
  },
  data: function() {
    //See if there are any notes stored and load them
    const notesJson = localStorage.getItem('notes');
    let notes = [];
    if (notesJson) {
      notes = JSON.parse(notesJson);
    }

    //See if there's a user account stored and load that
    const accountJson = localStorage.getItem('account');
    let authUser = false; //If the authUser isn't set, then we show the login page
    if (accountJson) {
      authUser = JSON.parse(accountJson);
    }

    return {
      isLoggedIn : !!authUser, //we can use isLoggedIn to control which parts of the app is shown
      authUser : authUser,
      notes : notes
    }
  },
  methods : {
    noteAdded : function(note){
      this.notes.unshift(note);
    },

    loggedIn : function(account) {
      //When the user logs in, update the state and save the user account to localstorage
      //In a real application, you'd never do this. You'd store maybe a token in a cookie
      //But we're doing this to demonstrate the vulnerability
      this.authUser = account;
      this.isLoggedIn = true;
      localStorage.setItem('account', JSON.stringify(account));
    },

    logout : function() {
      localStorage.removeItem('account');
      this.isLoggedIn = false;
    }
  }
}
</script>
<style>
@import "assets/css/style.css";
</style>