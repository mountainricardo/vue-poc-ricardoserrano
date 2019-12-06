<template>
  <div class="hello">
        <h1>Listado de convocatorias</h1>
        <ul id="calls">
          <li v-bind:key="k" v-for="(call, k) in calls">
            <h2>{{call.name}}</h2>
            <p>{{ call.description }}</p>
            <ul>
              <li v-bind:key="i" v-for="(merit, i) in merits
                .filter(x => x.callId === call.id)
                .sort(function(a,b){return Number(a.name.split(' ')[1]) - Number(b.name.split(' ')[1])} )">
                <h3>{{ merit.name }}</h3>
              </li>
            </ul>
          </li>
        </ul>
  </div>
</template>

<script>
import axios from 'axios'
// import mocks for templating
import calls from '../mocks/calls'
import merits from '../mocks/merits'

export default {
  name: 'HelloWorld',
  data () {
    return {
      calls: [],
      merits: [],
      response: ''
    }
  },
  mounted () {
    axios({ method: 'GET',
      'url': 'https://saviatest.azurewebsites.net/api/Calls',
      'headers': { 'Content-Type': 'application/json', 'Access-Control-Allow-Origin': '*' } })
      .then(result => {
        this.calls = result.data
      // console.log('results', this.calls)
      }, error => {
      // force hardcoded mock data just for developing web layer
        this.calls = calls
        this.merits = merits
        console.error(error)
      })
  },
  methods: { }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  width: 50%;
  text-align: left;
  padding: 1rem;
}
ul {
  list-style-type: none;
  padding: 0;
  &#calls{
    &>li{
      background-color: #ededed;
      margin-bottom: 1rem;
      padding: 1rem;
      h2, p{
        text-align: left;
      }
      & > ul > li {
        width: 100%;
        background-color: #9e9e9e;
        margin-bottom: .5rem;
      }
    }
  }
}
</style>
