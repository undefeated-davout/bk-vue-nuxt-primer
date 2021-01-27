<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <table>
      <tr>
        <th>Email</th>
        <td><input v-model="email" /></td>
        <td><button @click="delData">Click</button></td>
      </tr>
    </table>
    <hr />
    <ul v-for="(data, key) in json_data" :key="key">
      <li>
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
      message: 'axios sample.',
      json_data: {},
    }
  },
  created() {
    this.getData()
  },
  methods: {
    delData() {
      const delUrl = url + '/' + this.email + '.json'

      axios.delete(delUrl).then((re) => {
        this.message = this.email + 'を削除しました。'
        this.email = ''
        this.getData()
      })
    },
    getData() {
      axios
        .get(url + '.json')
        .then((res) => {
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
