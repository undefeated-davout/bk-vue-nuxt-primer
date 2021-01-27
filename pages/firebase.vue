<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <input v-model="find" />
    <button @click="getData">Click</button>
    <hr />
    <ul>
      <li>{{ json_data }}</li>
    </ul>
  </section>
</template>

<script>
const axios = require('axios')

const url =
  'https://プロジェクト.firebaseio.com/person.json?orderBy=%22$key%22&equalTo=%22' // ★

export default {
  data() {
    return {
      title: 'Axios',
      find: '',
      message: 'axios sample.',
      json_data: {},
    }
  },
  methods: {
    getData() {
      const idUrl = url + this.find + '%22'
      axios
        .get(idUrl)
        .then((res) => {
          this.message = 'get ID=' + this.find
          this.json_data = res.data
        })
        .catch(() => {
          this.message = 'ERROR!'
          this.json_data = {}
        })
    },
  },
}
</script>

<style>
ul {
  margin: 0px 10px;
  background-color: aliceblue;
}
li {
  padding: 10px;
  font-size: 16pt;
}
</style>
