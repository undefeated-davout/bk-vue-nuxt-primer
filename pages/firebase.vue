<template>
  <section class="container">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <ul v-for="(data, key) in json_data" :key="key">
      <li>{{ data.name }} ({{ data.age }}) [{{ key }}]</li>
    </ul>
  </section>
</template>

<script>
const axios = require('axios')

const url = 'https://プロジェクト.firebaseio.com/person.json' // サンプル用

export default {
  async asyncData() {
    const result = await axios.get(url)
    return { json_data: result.data }
  },
  data() {
    return {
      title: 'Axios',
      message: 'axios sample.',
    }
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
