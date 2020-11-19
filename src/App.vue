<template>
  <div id="app">
    <header class="header">
      <h1>Rock X Paper X Scissors</h1>

    </header>
    

    <div class="game">

      <div class="players"> {{ choices }} <p>{{ result }}</p> </div>

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
      result: '',

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
        return 'teste x teste'
      }
      else if (!this.cpu) {
        return this.player
      }
      else{
        console.log(this.result)
        return `${this.player} X ${this.cpu}`
      }    
    },    
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

      if(this.player == this.cpu){
        /*'Draw'*/
        this.result = 'Draw'
        this.scored("")
      }
      else if(this.player == 'Rock'){
        if(this.cpu == 'Paper') {
          /*'Lose'*/
          this.scored("Cpu")
        }
        else if(this.cpu == 'Scissors') {
          /*'Win'*/
          this.scored("Player")
        }
      }
      else if(this.player == 'Paper'){
        if(this.cpu == 'Scissors') {
          /*'Lose'*/
          this.scored("Cpu")
        }
        else if(this.cpu == 'Rock') {
          /*'Win'*/
          this.scored("Player")
        }
      }
      else if(this.player == 'Scissors'){
        if(this.cpu == 'Rock') {
          /*'Lose'*/
          this.scored("Cpu")
        }
        else if(this.cpu == 'Paper') {
          /*'Win'*/
          this.scored("Player")
        }
      }

    },

    scored(winner) {
      if(winner == 'Player'){
        this.scoreboard.player ++
        this.result = 'Win'
      }
      else if(winner == 'Cpu') {
        this.scoreboard.cpu ++
        this.result = 'Lose'
      }
      this.addHistoric()
      
    },

    addHistoric() {
      this.historic.push(this.choices)
    },

    


  }
}
</script>

<style>

body {
  margin: 0;
  background-color: #2f1a52;
}

li, p, ul, li{
  list-style: none;
  padding: 0;
  margin: 0;
}

:root {
  font-size: 62.5%; /*10px*/
}

#app {
  /*font-family: Avenir, Helvetica, Arial, sans-serif;*/
  font-family: 'Goldman', cursive;
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
  height: 10rem;
  width: 100%;

  grid-area: header;
}
.header h1 {
  font-size: 3.5rem;
}

.game {
  grid-area: game;

  height: calc(100vh - 20rem);
  width: 100vw;

  display: grid;
  grid-template-columns: 1fr 1fr 1fr minmax(20rem, 1fr);
  grid-template-areas: 
    "players players players right"
    "icon1 icon2 icon3 right"
  ;
}

.players {
  /*position: absolute;*/
  width: 100%;
  height: 5rem;
  background-color: rgba(119, 136, 153, .8);
  grid-area: players;

  font-size: 2.5rem;
}

.right {
  background-color: rgb(78, 78, 78);
  grid-area: right;

  font-size: 2rem;

  display: grid;
  grid-template-rows: 5rem 1fr;
  
  
}
.right p {
  font-size: 3.5rem;
}
.right ul {
  padding-top: 2rem;
}

.icon {
  width: 13rem;
  /*height: 100%;*/
  cursor: pointer;
}

.footer {
  background-color: brown;
  height: 10rem;
  width: 100%;

  position: fixed;
  bottom: 0;
  left: 0;

  font-size: 1.5rem;

  grid-area: footer;
}
</style>
