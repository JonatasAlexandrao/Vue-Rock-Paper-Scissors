<template>
  <div id="app">
    <header class="header">
      <h1>Rock X Paper X Scissors</h1>

    </header>
    

    <div class="game">

      <div class="players"> teste x teste </div>

      <img class="icon -rock" src="./img/rock.svg" alt="Rock (pedra)">
      <img class="icon -paper" src="./img/paper.svg" alt="Paper (papel)">
      <img class="icon -scissors" src="./img/scissors.svg" alt="Scissors (tesoura)">

      <aside class="right">
        <p>...</p>
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
  components: {}
}
</script>

<style>

body {
  margin: 0;
  background-color: #2f1a52;
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
