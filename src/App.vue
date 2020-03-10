<template>
  <div id="app">
    <button @click="onInputfile">import</button>
    {{file}}
  </div>
</template>

<script>
const csv = require('csv-parser')
const fs = require('fs')
export default {
  name: 'app',
  data () {
    return {
      file: {}
    }
  },
  methods: {
    onInputfile () {
      let results = []
      fs.createReadStream('./data.csv')
        .pipe(csv())
        .on('data', (data) => results.push(data))
        .on('end', () => {
          console.log(results)
        })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
