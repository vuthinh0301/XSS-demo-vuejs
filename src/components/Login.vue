<template>
  <div class="login">
    <input v-model="username" type="text" class="form-control" placeholder="Username">
    <br />
    <input v-model="password" type="password" class="'form-control" placeholder="Password">
    <br />
    <button v-on:click="login(username, password)" type="button">Login</button>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Login',
  data : function(){
    return {
      username: '',
      password: '',

      accounts: [
        {username: 'thinh', password: 'thinh', avatar: 'https://www.gravatar.com/avatar/123412341234?d=robohash'},
        {username: 'hai', password: 'hai', avatar: 'https://www.gravatar.com/avatar/432143214321?d=robohash'},
        {username: 'lam', password: 'lam', avatar: 'https://www.gravatar.com/avatar/432143211111?d=robohash'},
        {username: 'trieu', password: 'trieu', avatar: 'https://www.gravatar.com/avatar/43214322211?d=robohash'}
      ]
    }
  },
  methods: {

    login: function(username, password){
      let account = false;
      for (let checkAccount of this.accounts) {
        if (username === checkAccount.username && checkAccount.password === password) {
          account = checkAccount
          break;
        }
      }
      if (account === false) {
        alert("Username or password is incorrect!");
        return;
      }
      //Let the parent component know we logged in
      this.$emit("loggedIn", account);
    }
  }
}
</script>
