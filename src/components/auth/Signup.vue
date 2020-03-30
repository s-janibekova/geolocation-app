<template>
    <div class="signup container">
        <form @submit.prevent="onSubmit" class="card-panel">
            <h2 class="center deep-pink-text">Регистрация</h2>
            <div class="field">
                <label for="email">Email</label>
                <input type="email" name="email" v-model="email">
            </div>
            <div class="field">
                <label for="password">Пароль</label>
                <input type="password" name="password" v-model="password">
            </div>
            <div class="field">
                <label for="alias">Сокращение</label>
                <input type="text" name="alias" v-model="alias">
            </div>
            <p class="red-text" v-if="feedback">{{ feedback }}</p>
            <button class="btn">Войти</button>
        </form>
    </div>
</template>

<script>
import slugify from 'slugify'
import db from '@/firebase/init'
import firebase from 'firebase'
export default {
  name: 'Signup',
  data () {
    return {
      email: null,
      password: null,
      alias: null,
      slug: null,
      feedback: null
    }
  },
  methods: {
    onSubmit () {
      if (this.alias && this.email && this.password) {
        this.slug = slugify(this.alias, {
          replacement: '-',
          remove: /[$*_+~.()'"!]/g,
          lower: true
        })
        let ref = db.collection('users').doc(this.slug)
        ref.get().then(response => {
          if (response.exists) {
            this.feedback = 'имя уже существует'
          } else {
            firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
              .then(user => {
                ref.set({
                  alias: this.alias,
                  geolocation: null,
                  user_id: user.uid
                })
              }).then(() => {
                this.$router.push({ name: 'Gmap' })
              })
              .catch(error => {
                console.log(error)
                this.feedback = error.message
              })
            this.feedback = ''
          }
        })
      } else {
        this.feedback = 'Вы не ввели имя пользователя'
      }
    }
  }
}
</script>

<style scoped>
.signup {
    max-height: 400px;
    max-width: 500px;
    margin-top: 3rem;
}
.btn {
    margin-left: 12rem;
    margin-top: 2rem;
}
</style>
