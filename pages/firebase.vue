<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <input v-model="find" />
    <button @click="getData">Click</button>
    <hr />
    <ul>
      <li v-for="(data, key) in json_data" :key="key">
        <strong>{{ key }}</strong
        ><br />{{ data }}
      </li>
    </ul>
  </section>
</template>

<script>
const axios = require('axios')

const url = 'https://プロジェクト.firebaseio.com/person.json?orderBy=%22age%22' // ★

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
      const range = this.find.split(',')
      const ageUrl = url + '&startAt=' + range[0] + '&endAt=' + range[1]
      axios
        .get(ageUrl)
        .then((res) => {
          this.message = 'get: ' + range[0] + ' < age < ' + range[1]
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
