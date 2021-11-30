<template>
  <div class="container w-screen h-screen m-0 p-0" style="margin: 0">
    <h1>Welcome</h1>
    <div class="main-content mx-auto w-full h-3/4">
      <div class="score flex rounded-lg border border-gray-300 p-3 w-1/2 mx-auto">
        <div class="rock-img w-2/3">
          <img src="./assets/logo.svg" alt="" />
        </div>
        <div
          class="score-content w-1/3 bg-white rounded-lg flex flex-col justify-center items-center"
        >
          <p class="text-1xl font-bold uppercase">score</p>
          <p class="text-6xl font-bold" >{{score}}</p>
        </div>
      </div>

      <div v-if="!playerMakeChoice" class="container-game w-1/2 flex mx-auto mt-10">
        <div class="container-paper"  @click="getChoicePlayer('paper')" :name="paper">
          <img src="./assets/icon-paper.svg" alt="" />
        </div>
        <div class="container-rock" @click="getChoicePlayer('rock')" :name="rock">
          <img src="./assets/icon-rock.svg" alt="" />
        </div>
        <div class="container-scissor" @click="getChoicePlayer('scissor')" id="scissor">
          <img src="./assets/icon-scissors.svg" alt="" />
        </div>
      </div>

      <div v-else class="container-roundplay flex mt-10 flex justify-evenly w-3/4 mx-auto h-3/4">
        <div class="container-handPlayer flex flex-col justify-evenly items-center  w-1/3 ">
          <h2 class="uppercase font-bold text-white  text-center w-auto">you picked</h2>
          <div v-if='playerChoice =="paper"' class="containerPlayer-paper " :name="paper">
            <img src="./assets/icon-paper.svg " alt="" />
          </div>
          <div v-else-if='playerChoice =="rock"' class="containerPlayer-rock " :name="rock">
            <img src="./assets/icon-rock.svg" alt="" />
          </div>
          <div v-else-if='playerChoice =="scissor"' class="containerPlayer-scissor " :name="scissor">
            <img src="./assets/icon-scissors.svg" alt="" />
          </div>
        </div>
        <div v-if="displayResult" class="result-container w-1/3 flex flex-col justify-center items-center ">
          <div v-if='result =="win"' class="win-container"><p class="uppercase mb-3 text-white text-3xl font-bold">you win</p> <button @click="restart()" class="uppercase rounded-lg px-9 py-2 bg-white btn-color text-xs font-bold" >play again</button></div>
          <div v-else-if='result =="lose"' class="lose-container"><p class="uppercase mb-3 text-white text-3xl font-bold ">you Lose</p> <button @click="restart()" class="uppercase rounded-lg px-9 py-2 bg-white text-red-400 text-xs font-bold" >play again</button></div>
          <div v-else class="lose-container"><p class="uppercase mb-3 text-white text-3xl font-bold ">Equality</p> <button @click="restart()" class="uppercase rounded-lg px-9 py-2 bg-white text-blue-400 text-xs font-bold" >play again</button></div>
          <!-- <div class="lose-container"></div> -->
        </div>
        <div  class="container-handHouse flex flex-col justify-evenly items-center  w-1/3 ">
          <h2 class="uppercase font-bold text-white  text-center w-auto  ">the house picked</h2>
          <div v-if='houseChoice == "paper"' class="containerPlayer-paper " :name="paper">
            <img src="./assets/icon-paper.svg" alt="" />
          </div>
          <div v-else-if='houseChoice == "rock"'  class="containerPlayer-rock " :name="rock">
            <img src="./assets/icon-rock.svg" alt="" />
          </div>

          <div v-else-if='houseChoice == "scissor"' class="containerPlayer-scissor " :name="scissor">
            <img src="./assets/icon-scissors.svg" alt="" />
          </div>
          <div v-else-if="houseChoice === ''" class="handEmpty"></div>
        </div>
      </div>
    </div>
  </div>
  <button class="btn-rules border rounded-lg px-7 py-1 text-white uppercase">
    rules
  </button>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    // HelloWorld
  },

  data() {
    return {
      playerMakeChoice: false,
      playerChoice: "",
      houseChoice:"",
      possibleChoice : ["paper","scissor","rock"],
      result:"",
      displayResult:false,
      score:0
    };
  },

  methods: {
    getChoicePlayer(str){
      this.playerChoice = str
      this.playerMakeChoice = true
      setTimeout(function(){
       this.houseChoice =  this.possibleChoice[Math.floor(Math.random() * this.possibleChoice.length)]
       this.checkWinner()
       this.displayResult = true
      }.bind(this),1000)
    },

    checkWinner() {
      switch (this.playerChoice) {
        case "paper":
          if(this.houseChoice == "scissor"){
            this.result = "lose"
            this.score-=1
          }else if(this.houseChoice == "rock"){
            this.result = "win"
            this.score+=1
          }else{
            this.result = "equality"
          }    
          break;
        case "scissor":
          if(this.houseChoice == "rock"){
            this.result = "lose"
            this.score-=1
          }else if(this.houseChoice == "paper"){
            this.result = "win"
            this.score+=1
          }else{
            this.result = "equality"
          }
          break;
        case "rock":
          if(this.houseChoice == "paper"){
            this.result = "lose"
            this.score-=1
          }else if(this.houseChoice == "scissor"){
            this.result = "win"
            this.score+=1
          }else{
            this.result = "equality"
          }
          break;

      
        default:

          break;
      }
    },
    restart(){
      this.playerMakeChoice= false
      this.playerChoice= ""
      this.houseChoice=""

      this.result=""
      this.displayResult=false
    }
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  background-color: rgb(26, 41, 74);
}
.btn-color{
  color:rgb(26, 41, 74);
}
.container-paper,
.container-rock,
.container-scissor {
  height: 150px;
  width: 150px;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 10px;
  border-radius: 50%;
  border: 15px solid;
  box-shadow: inset 0 4px 0 0 rgba(0, 0, 0, 0.2);
}

.container-paper {
  border-color: rgb(6, 170, 235);
  position: absolute;
  left: 15%;
  top: 7%;
}
.container-rock {
  border-color: rgba(248, 63, 30, 0.801);
  position: absolute;
  bottom: 40px;
  left: 42%;
}
.container-scissor {
  border-color: rgb(245, 163, 55);
  position: absolute;
  left: 67%;
  top: 7%;
}

.container-game {
  background-image: url("./assets/bg-triangle.svg");
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
  position: relative;
}

.btn-rules {
  position: absolute;
  right: 20px;
  bottom: 20px;
}

// Partie jeu

.containerPlayer-paper,
.containerPlayer-rock,
.containerPlayer-scissor {
  height: 200px;
  width: 200px;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 10px;
  border-radius: 50%;
  border: 20px solid;
  box-shadow: inset 0 4px 0 0 rgba(0, 0, 0, 0.2);
}

.containerPlayer-paper {
  border-color: rgb(6, 170, 235);
}
.containerPlayer-rock {
  border-color: rgba(248, 63, 30, 0.801);
}
.containerPlayer-scissor {
  border-color: rgb(245, 163, 55);
}



.handEmpty {
  height: 150px;
  width: 150px;
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 50%;
  margin: 0 auto;
}

.circle {
  height:100px;
  width:100px;
  border-radius:50%;
  background-color:red;
  
  position:relative;
  top:100px;
  left:300px;
  
  -webkit-transition:height .25s ease, width .25s ease;
  transition:height .25s ease, width .25s ease;
  
  -webkit-transform:translate(-50%,-50%);
  transform:translate(-50%,-50%);
}

.circle:hover{
  height:150px;
  width:150px;
}

.circle:before,
.circle:after {
  content:'';
  display:block;
  position:absolute;
  top:0; right:0; bottom:0; left:0;
  border-radius:50%;
  border:1px solid red;
}

.circle:before {
  -webkit-animation: ripple 2s linear infinite;
  animation: ripple 2s linear infinite;
}
.circle:after {
  -webkit-animation: ripple 2s linear 1s infinite;
  animation: ripple 2s linear 1s infinite;
}

.circle:hover:before,
.circle:hover:after {
  -webkit-animation: none;
  animation: none;
}

@-webkit-keyframes ripple{
  0% {-webkit-transform:scale(1); }
  75% {-webkit-transform:scale(1.75); opacity:1;}
  100% {-webkit-transform:scale(2); opacity:0;}
}

@keyframes ripple{
  0% {transform:scale(1); }
  75% {transform:scale(1.75); opacity:1;}
  100% {transform:scale(2); opacity:0;}
}
</style>
