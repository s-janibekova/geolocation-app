<template>
    <nav class="nav-extended">
      <div class="container">
    <div class="nav-wrapper">
      <a href="#!" class="brand-logo">Welcome=)</a>
      <ul class="right hide-on-med-and-down">
        <li><router-link :to="{name: 'Signup'}">Регистрация</router-link></li>
        <li><router-link :to="{name: 'Login'}">Логин</router-link></li>
        <li><a @click="logout">Выйти</a></li>
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
    }
  },
  methods: {
    logout () {
      firebase.auth().signOut().then(() => {
        this.$router.push({ name: 'Signup' })
      })
    }

  }
}
</script>
<style scoped>

</style>
