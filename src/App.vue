<template>
  <div id="app">
    <header class="header">
      <h1>Rock X Paper X Scissors</h1>

    </header>
    
    <div class="result" :class="enableTeste" @click="enable=false" >
      <p>{{ result }}</p>
    </div>

    <div class="game">

      <div class="players"> {{ choices }} </div>

      <div class="icons">
        <div>
          <img class="icon -rock" :class="classAnimateRock" 
            src="./img/rock.svg" alt="Rock (pedra)" 
            @click="selectOption(0)" 
            @mouseover="animeHeartBeat('rock')" 
            @mouseout="animeHeartBeat('rock')"
          >

          <img class="icon -paper" :class="classAnimatePaper"
            src="./img/paper.svg" alt="Paper (papel)" 
            @click="selectOption(1)"
            @mouseover="animeHeartBeat('paper')" 
            @mouseout="animeHeartBeat('paper')"
          >
          <img class="icon -scissors" :class="classAnimateScissors"
            src="./img/scissors.svg" alt="Scissors (tesoura)" 
            @click="selectOption(2)"
            @mouseover="animeHeartBeat('scissors')" 
            @mouseout="animeHeartBeat('scissors')"
          >
        </div>
      </div>

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
      animate: true,
      //classAnimate: '',
      classAnimateRock: '',
      classAnimatePaper: '',
      classAnimateScissors: '',
      enable: false,


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
    enableTeste() {
      if(this.enable){
        return 'enable animate__animated animate__fadeIn'
      }
      else {
        return ''
      }
    }

  },

  methods: {
    animeHeartBeat(teste) {

      if(this.animate){

        if(this.classAnimateRock == '' && teste == 'rock') {
          this.classAnimateRock = 'animate__animated animate__heartBeat animate__infinite infinite'
        }          
        else{
          this.classAnimateRock = ''
        }

        if(this.classAnimatePaper == '' && teste == 'paper') {
          this.classAnimatePaper = 'animate__animated animate__heartBeat animate__infinite infinite'
        }          
        else{
          this.classAnimatePaper = ''
        }

        if(this.classAnimateScissors == '' && teste == 'scissors') {
          this.classAnimateScissors = 'animate__animated animate__heartBeat animate__infinite infinite'
        }          
        else{
          this.classAnimateScissors = ''
        }
      
      }
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
      this.enable = true
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
  background-color: #2d3047;
}

li, p, ul, li{
  list-style: none;
  padding: 0;
  margin: 0;
}
a {
  color:cornsilk;
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

.result { 

  display: none;
  position: absolute;
  width: 100vw;
  height: 100%;

  font-size: 10rem;
  background-color: rgba(0, 0, 0, .6);
  z-index: 1;
  
}
.result p {
  
  position: fixed;
  width: 100%;
  left: 50%;
  top: 40%;
  transform: translateX(-50%) translateY(-50%);

  background-color: rgba(255, 255, 255, .1);
  user-select: none;

}
.result.enable {
  display: block;
}

.header {
  background-color: #64113f;
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
    "icon icon icon right"
  ;
}

.icons {
  position: relative;
  grid-area: icon;
  height: calc(100vh - 20rem);
}
.icons > div {
  /*background-color: aqua;*/
  position: absolute;
  transform: translateX(-50%) translateY(-50%);
  left: 50%;
  top: 50%;
  width: 100%;
}

.players {
  /*position: absolute;*/
  width: 100%;
  height: 5rem;
  background-color: #f7cacd;
  color: #022b3a;
  grid-area: players;

  font-size: 3rem;
}

.right {
  background-color: #022b3a;
  color: #f7cacd;
  grid-area: right;

  font-size: 2rem;

  display: grid;
  grid-template-rows: 5rem 1fr;
  user-select: none;
  
}
.right ul {
  padding-top: 2rem;
}
.right p {
  font-size: 4rem;
}

.icon {
  width: 13rem;
  padding: 0 10px;
  /*height: 100%;*/
  cursor: pointer;
}

.footer {
  background-color: #64113f;
  height: 10rem;
  width: 100%;

  position: fixed;
  bottom: 0;
  left: 0;

  font-size: 1.5rem;

  grid-area: footer;
}
</style>
