<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <table>
      <tr>
        <th>Email</th>
        <td><input v-model="email" /></td>
      </tr>
      <tr>
        <th>Name</th>
        <td><input v-model="username" /></td>
      </tr>
      <tr>
        <th>Age</th>
        <td><input v-model="age" type="number" /></td>
      </tr>
      <tr>
        <th>Tel</th>
        <td><input v-model="tel" /></td>
      </tr>
      <tr>
        <th></th>
        <td>
          <button @click="addData">Click</button>
        </td>
      </tr>
    </table>
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

const url = 'https://プロジェクト.firebaseio.com/person' // ★

export default {
  data() {
    return {
      title: 'Axios',
      email: '',
      username: '',
      tel: '',
      age: 0,
      message: 'axios sample.',
      json_data: {},
    }
  },
  created() {
    this.getData()
  },
  methods: {
    addData() {
      const addUrl = url + '/' + this.email + '.json'
      const data = {
        name: this.username,
        age: this.age,
        tel: this.tel,
      }
      axios.put(addUrl, data).then((re) => {
        this.email = ''
        this.username = ''
        this.age = 0
        this.tel = ''
        this.getData()
      })
    },
    getData() {
      axios
        .get(url + '.json')
        .then((res) => {
          this.message = 'get all data.'
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
