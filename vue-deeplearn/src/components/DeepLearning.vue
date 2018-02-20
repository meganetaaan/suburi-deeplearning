<template>
  <div class="deepLearning">hoge</div>
</template>

<script>
import * as dl from 'deeplearn'
console.log(dl)

export default {
  name: 'DeepLearning',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    const a = dl.tensor1d([1, 2, 3])
    const b = dl.scalar(2)

    const result = a.add(b)
    result.data().then(data => console.log(data))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
