<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
  </section>
</template>

<script>
import firebase from 'firebase'

export default {
  data() {
    return {
      title: 'Auth',
      message: 'this is message.',
    }
  },
  created() {
    const config = {
      // ●各自の設定を記述
      apiKey: '……キー……',
      authDomain: 'プロジェクト.firebaseapp.com',
      databaseURL: 'https://プロジェクト.firebaseio.com',
      projectId: 'プロジェクト',
      storageBucket: 'プロジェクト.appspot.com',
      messagingSenderId: '……ID……',
    }
    firebase.initializeApp(config)

    const provider = new firebase.auth.GoogleAuthProvider()
    const self = this
    firebase
      .auth()
      .signInWithPopup(provider)
      .then(function (result) {
        self.message = result.user.displayName + ', ' + result.user.email
      })
  },
}
</script>

<style></style>
