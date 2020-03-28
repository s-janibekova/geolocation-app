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
            <p class="red-text" v-if="feedback">{{ feedback }}</p>
            <button class="btn" type="submit">Войти</button>
        </form>
    </div>
</template>

<script>
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
      if (this.email && this.password) {
        this.feedback = 'good'
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
