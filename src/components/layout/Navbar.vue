<template>
    <nav class="nav-extended">
      <div class="container">
    <div class="nav-wrapper">
      <router-link :to="{ name: 'Gmap' }" class="brand-logo">Welcome=)</router-link>
      <ul class="right hide-on-med-and-down">
        <li v-if="!user"><router-link :to="{name: 'Signup'}">Регистрация</router-link></li>
        <li v-if="!user"><router-link :to="{name: 'Login'}">Логин</router-link></li>
        <li v-if="user">{{ user.email }}</li>
        <li v-if="user"><a @click="logout">Выйти</a></li>
      </ul>
    </div>
    <div class="nav-content">

    </div>
    </div>
   </nav>
</template>

<script>
import firebase from 'firebase'
export default {
  name: 'Navbar',
  data () {
    return {
      user: null
    }
  },
  methods: {
    logout () {
      firebase.auth().signOut().then(() => {
        this.$router.push({ name: 'Signup' })
      })
    }
  },
  created () {
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.user = user
      } else {
        this.user = null
      }
    })
  }
}
</script>
<style scoped>

</style>
