<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title>Trello clone</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items v-if="!user">
        <v-btn flat :to="{name: 'login'}">Login</v-btn>
        <v-btn flat :to="{name: 'signup'}">SignUp</v-btn>
      </v-toolbar-items>
      <v-toolbar-items v-if="user">
        <v-layout justify-content align-center>
          <v-avatar
            size="40"
            color="grey lighten-4">
            <img :src="user.user.imageUrl"  alt="avatar">
          </v-avatar>
          <h3>Hello {{user.user.username}}!     </h3>
        </v-layout>
        <v-btn @click to="/profile" flat>Profile</v-btn>
        <v-btn flat @click="logout">LogOut</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-content>

      <router-view/>
    </v-content>
    <v-footer app>
      <span> 2019 - Programowanie aplikacji webowych- grupa II</span>
    </v-footer>
  </v-app>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  name: 'App',
  data() {
    return {
      fixed: false,
    };
  },
  computed: {
    ...mapState('auth', { user: 'payload' }),

  },

  methods: {
    ...mapActions('auth', { authLogout: 'logout' }),

    logout() {
      this.authLogout().then(() => this.$router.push('/login'));
    },

  },
};
</script>
