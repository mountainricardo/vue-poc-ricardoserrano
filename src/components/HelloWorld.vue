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
                <span class="score" v-text="merit.score * factor"></span>
                <div class="total-score">
                  <h4 class="total-heading">TotalScore</h4>
                  <span class="score-factor" v-text="factor"></span>
                  <input class="score-input" v-model="merit.score" placeholder="User score"/>
                </div>
              </li>
            </ul>
          </li>
        </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      calls: [],
      merits: [],
      factor: 2,
      response: ''
    }
  },
  mounted () {
    // Configure axios instance for saviatest server
    const axiosInstance = axios.create({
      baseURL: 'https://saviatest.azurewebsites.net/api'
    })
    // Executes concurrent requests
    axios.all([
      axiosInstance.get('/Calls'),
      axiosInstance.get('/Merits')
    ])
      .then(response => {
        console.log('Calls', response[0].data)
        console.log('Merits', response[1].data)
        this.calls = response[0].data
        this.merits = response[1].data
      })
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
body{
  margin: 0px;
  padding: 0px;
}
h1{
  font-size: 2.2rem;
}
h3 {
  width: 50%;
  text-align: left;
  padding: 1rem;
}
@media screen and (min-width: 990px){
  h1{
    text-align: left;
    width: 75%;
    font-size: 3rem;
    margin: .5em auto;
    padding: 0;
  }
}
ul {
  list-style-type: none;
  padding: 0;
  box-sizing: border-box;
  &#calls{
    &>li{
      width: 100%;
      box-sizing: border-box;
      background-color: #ededed;
      padding: 1rem;
      margin-bottom: 1.5rem;
      h2{
        text-align: left;
        width: 100%;
        margin: 0 0 0 0;
      }
      p{
        width: 100%;
        text-align: left;
        line-height: 1.5em;
        margin: .5em 0;
      }
      & > ul {
        & > li{
          width: 100%;
          background-color: #9e9e9e;
          margin-bottom: 1rem;
          display: grid;
          grid-template-columns: 50% 50%;
          align-items: start;
          justify-content: space-between;
          &:nth-child(odd) { background: #dbdbdb; }
          h3{
            margin-top:0;
          }
          span.score {
            max-width: 40%;
            font-size: 1.2em;
            text-align: right;
            margin: .8em 1.5em .8em auto;
            &:after{
            content: "puntos";
            margin-left: .5em;
          }
          }
        }
      }
    }
  }
  @media screen and (min-width: 990px){
    &#calls{
      display:flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      h2{
        font-size: 2.2em;
      }
      p{
        font-size: 1.5em;
      }
      & > li{
        width: 75%;
        padding: 3rem;
        & > ul {
          display: grid;
          width: 100%;
          grid-template-columns: 50% 50%;
          align-items: start;
          justify-content: space-between;

          & > li{
            width: calc( 100% - 2rem);
            background-color: #dbdbdb;
            margin-bottom: 2rem;
            &:nth-child(even) {
              margin-left: auto;
            }
            h3{
              font-size: 1.7em;
              margin-top: 0;
              width: 100%;
            }
          span.score {
            max-width: 40%;
            font-size: 1.2em;
            text-align: right;
            margin: 1.15em 1.5em .8em auto;
           }
          }
        }
      }
    }
  }

}
</style>
