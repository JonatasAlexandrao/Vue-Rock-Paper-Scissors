<template>
  <div id="app">
    <header class="header">
      <h1>Rock X Paper X Scissors</h1>

    </header>
    

    <div class="game">

      <div class="players"> {{ choices }} </div>

      <img class="icon -rock" src="./img/rock.svg" alt="Rock (pedra)" @click="selectOption(0)">
      <img class="icon -paper" src="./img/paper.svg" alt="Paper (papel)" @click="selectOption(1)">
      <img class="icon -scissors" src="./img/scissors.svg" alt="Scissors (tesoura)" @click="selectOption(2)">

      <aside class="right">
        <p>{{ scoreboard.player }} X {{ scoreboard.cpu }}</p>
        
        <ul>
          <li v-for="(h, index) in historic" :key="index">{{ h }}</li>
        </ul>
      </aside>
    </div>

    <footer class="footer">
      <a href="https://www.vecteezy.com/free-vector/rock-paper-scissors">Rock Paper Scissors Vectors by Vecteezy</a>
    </footer>
    
  </div>
</template>

<script>


export default {
  name: 'App',

  components: {},

  data() {
    return {
      player: '',
      cpu: '',

      game: [
        {id: 0, option: 'Rock'},
        {id: 1, option: 'Paper'},
        {id: 2, option: 'Scissors'}
      ],

      scoreboard: {
        player: 0,
        cpu: 0
      },

      historic: []
    }
  },

  computed: {
    choices() {
      if(!this.player){
        return ''
      }
      else if (!this.cpu) {
        return this.player
      }
      else{
        return `${this.player} X ${this.cpu}`
      }    
    }
  },

  methods: {
    testeClick() {
      console.log('clicou')
    },

    selectOption(option) {
      
      this.player = this.game[option].option
      this.selectcpu(Math.floor(Math.random() * 3))

    },

    selectcpu(option) {
      console.log(option)
      this.cpu = this.game[option].option

      this.gameLogic()
    },

    gameLogic() {

      let result = ''

      if(this.player == this.cpu){
        result = 'Draw'
        this.scored("")
      }
      else if(this.player == 'Rock'){
        if(this.cpu == 'Paper') {
          result = 'Lose'
          this.scored("Cpu")
        }
        else if(this.cpu == 'Scissors') {
          result = 'Win'
          this.scored("Player")
        }
      }
      else if(this.player == 'Paper'){
        if(this.cpu == 'Scissors') {
          result = 'Lose'
          this.scored("Cpu")
        }
        else if(this.cpu == 'Rock') {
          result = 'Win'
          this.scored("Player")
        }
      }
      else if(this.player == 'Scissors'){
        if(this.cpu == 'Rock') {
          result = 'Lose'
          this.scored("Cpu")
        }
        else if(this.cpu == 'Paper') {
          result = 'Win'
          this.scored("Player")
        }
      }

      console.log(result)


    },

    scored(winner) {
      if(winner == 'Player'){
        this.scoreboard.player ++
      }
      else if(winner == 'Cpu') {
        this.scoreboard.cpu ++
      }
      this.addHistoric()
      
    },

    addHistoric() {
      this.historic.push(this.choices)
    }


  }
}
</script>

<style>

body {
  margin: 0;
  background-color: #2f1a52;
}

li {
  list-style: none;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #d1d1d1;
  

  position: relative;
  display: grid;
  grid-template-areas: 
  "header header header header"
  "game game game game"
  "footer footer footer footer"
  ;
}

.header {
  background-color: brown;
  height: 100px;
  width: 100%;

  grid-area: header;
}

.game {
  grid-area: game;

  height: calc(100vh - 200px);
  width: 100vw;

  display: grid;
  grid-template-columns: 1fr 1fr 1fr minmax(200px, 1fr);
  grid-template-areas: 
    "players players players right"
    "icon1 icon2 icon3 right"
  ;
}

.right {
  background-color: rgb(78, 78, 78);
  
  /*height: 100%;*/

  grid-area: right;
}
.players {
  /*position: absolute;*/
  width: 100%;
  height: 50px;
  background-color: rgba(119, 136, 153, .8);
  grid-area: players;
}

.icon {
  width: 130px;
  /*height: 100%;*/
  cursor: pointer;

  

}



.footer {
  background-color: brown;
  height: 100px;
  width: 100%;

  position: fixed;
  bottom: 0;
  left: 0;

  /*position: absolute;
  bottom: 0;*/

  grid-area: footer;
}
</style>
