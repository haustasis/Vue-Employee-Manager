<template>
  <nav>
    <div class="nav-wrapper green">
      <div class="container">
        <router-link to="/" class="brand-logo">Employee Manager</router-link>
        <ul class="right">
          <li v-if="isLoggedIn">
            <span class="email black-text">{{currentUser}}</span>
          </li>
          <li>
            <router-link v-if="isLoggedIn" to="/">Dashboard</router-link>
          </li>
          <li>
            <router-link v-if="!isLoggedIn" to="/login">Login</router-link>
          </li>
          <li>
            <router-link v-if="!isLoggedIn" to="/register">Register</router-link>
          </li>
          <li>
            <button v-if="isLoggedIn" v-on:click="logout" class="btn black">Logout</button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
import firebase from "firebase";
export default {
  name: "navbar",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false,
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedIn = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    logout: function () {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.go({ path: this.$router.path });
        });
    },
  },
};
</script>

<style scoped>
.email {
  padding-right: 10px;
}
</style>