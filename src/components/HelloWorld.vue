<template>
  <div class="hello">
        <h1>Listado de convocatorias</h1>
        <!-- Creates a Calls list -->
        <ul id="calls">
          <!-- Iterates on Calls model -->
          <li v-bind:key="call.id" v-for="(call) in calls">
            <h2>{{call.name}}</h2>
            <p>{{ call.description }}</p>
            <!-- For each call creates a Merits list -->
            <ul>
              <!-- iterates on Merits model for each Call and sorts them-->
              <li v-bind:key="i" v-for="(merit, i) in merits
                .filter(x => x.callId === call.id)
                .sort(function(a,b){return Number(a.name.split(' ')[1]) - Number(b.name.split(' ')[1])} )">
                <h3>{{ merit.name }}</h3>
                <span class="score" v-text="merit.score * factor"></span>
                <div class="total-container">
                  <h4 class="total-heading">TotalScore</h4>
                  <!-- Places total score for responsiveness -->
                  <div class="total-score">
                    <label class="score-factor" v-text="factor" :for="'merit_' + call.id + '_' + i"></label>
                    <input :id="'merit_' + call.id + '_' + i" class="score-input" type="number" v-model.number="merit.score" placeholder="User score"/>
                  </div>
                </div>
              </li>
            </ul>
          </li>
        </ul>
        <div class="save-button">
          <button>Guardar</button>
        </div>
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
    // Configures axios instance for saviatest server
    const axiosInstance = axios.create({
      baseURL: 'https://saviatest.azurewebsites.net/api'
    })
    // Executes concurrent requests
    axios.all([
      axiosInstance.get('/Calls'),
      axiosInstance.get('/Merits')
    ])
      .then(response => {
        // console.log('Calls', response[0].data)
        // console.log('Merits', response[1].data)
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
  text-align: left;
  padding: 0;
}
ul{
  list-style-type: none;
  padding: 0;
  box-sizing: border-box;
}
.save-button{
  button{
    background-color: #333;
    color: #fff;
    font-size: 1.7em;
    padding: .5em 1em;
    width: 100%;
    border: 0;
  }
}
@media screen and (min-width: 1024px){
  h1{
    text-align: left;
    width: 77%;
    font-size: 3rem;
    margin: .5em auto;
    padding: 0;
  }
  .save-button{
    width:77%;
    margin: 1.5em auto;
    button{
      width: auto;
      float: right;
      border-radius: .2em;
      cursor: pointer;
    }
  }
}
  #calls{
    // width: 100%;
    margin-bottom: 0;
    &>li{
      width: 100%;
      box-sizing: border-box;
      background-color: #ededed;
      padding: 1rem;
      margin-bottom: 1.5rem;
      &:last-child{
        margin-bottom: 0;
      }
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
          padding: 1em;
          box-sizing: border-box;
          background-color: #9e9e9e;
          margin-bottom: 1rem;
          display: grid;
          grid-template-columns: 50% 50%;
          align-items: start;
          justify-content: space-between;
          &:nth-child(odd) { background: #dbdbdb; }
          h3{
            margin: 0 0 1.2em 0;
          }
          span.score {
            max-width: 40%;
            font-size: 1.2em;
            text-align: right;
            margin: 0 0 0 auto;
            max-width: 60%;
            &:after{
            content: "puntos";
            margin-left: .5em;
            }
          }
          .total-container{
            display: grid;
            grid-template-columns: 100%;
            grid-column-end: span 2;
          }
          h4{
            text-align: left;
            font-size: 1.17em;
            padding: 0;
            margin: 0;
            font-weight: normal;
          }
          .total-score{
            border-width: 0px;
            text-align: left;
            margin: 1em auto 0 auto;
            max-width: calc( 100% - 2em);
            .score-factor{
              font-size: 1.7em;
              margin-left: 1em;
              &:after{
                content: '*';
                margin: 0 .4em;
              }
            }
            .score-input{
              border: 0;
              font-size: 1.17em;
              padding: .3em .5em;
              max-width: 50%;
            }
          }
        }
      }
    }
  }

  @media screen and (min-width: 1024px){
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
        width: 77%;
        padding: 1.5rem 1.56%;
        & > ul {          display: grid;
          width: 100%;
          grid-template-columns: 50% 50%;
          align-items: start;
          justify-content: space-between;

          & > li{
            width: 98.4%;
            background-color: #dbdbdb;
            margin-bottom: 2rem;
            grid-template-columns: 35% 65%;
            padding: 1em 4%;
            &:nth-child(even) {
              margin-left: auto;
            }
            h3{
              font-size: 1.5em;
              margin-top: 0;
              width: 100%;
            }
            .total-container{
              display: flex;
              margin: 0;
            }
            h4{
              font-size: 1.5em;
              max-width: auto;
            }
            .total-score{
              max-width: auto;
              margin: 0 0 1em 0;
              .score-factor{
                &:before{
                  content: '=';
                  position: relative;
                  left: -0.5em;
                }
              }
            }
          }
        }
      }
    }
  }
</style>
