<template>
  <div class="outer">
    <div class="container d-flex flex-column justify-content-center align-items-center">
      <h1 class="mt-5 text-white">Tic toc toe Game</h1>
      <div class="mt-5">
          <h2 
          v-if="isCross"
          class="text-center mb-5 text-danger">Cross turn</h2>
          <h2 
          v-if="!isCross"
          class="text-center mb-5 text-primary">Circle turn</h2>

            <div class="grid">
                <div v-for="(element, index) in boxes"
                :key="index"
                >
                    <Icon
                    :iconName="element"
                    @click="handleClick(index)"
                    />
                </div>
            </div> 
            <div class="d-flex justify-content-center mt-4">
              <button
              @click="reset"
              class="btn btn-lg btn-danger fw-bold">Restart game</button>
            </div>        
      </div>
      
    </div>    
  </div>
</template>

<script>
import Icon from "./components/icon";
import Alert from "sweetalert2/dist/sweetalert2.js"

export default {
  components:{
    Icon
  },
  data(){
    return{
      isCross: false,
      winMessage: '',
      boxes: new Array(9).fill('empty')
    }
  },
  watch:{
    winMessage: function(message){
      if(message){
        this.showDialog()
      }
    }
  },
  methods:{
    handleClick(index){
      if(this.winMessage){
        return this.showDialog()
      }
      if(this.boxes[index] === "empty"){
        this.boxes[index] = this.isCross ? "cross" : "circle" 
        this.isCross = !this.isCross
      }else{
        return Alert.fire("Already filled...")
      }
      this.checkWinner()
    },
    reset(){
      this.winMessage = ""
      this.boxes = new Array(9).fill("empty")
      this.isCross = false
    },
    checkWinner(){
      if(this.boxes[0] === this.boxes[1] && this.boxes[0] === this.boxes[2] && this.boxes[0] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[3] === this.boxes[4] && this.boxes[3] === this.boxes[5] && this.boxes[3] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[6] === this.boxes[7] && this.boxes[6] === this.boxes[8] && this.boxes[6] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[0] === this.boxes[3] && this.boxes[0] === this.boxes[6] && this.boxes[0] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[1] === this.boxes[4] && this.boxes[1] === this.boxes[7] && this.boxes[1] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[2] === this.boxes[5] && this.boxes[2] === this.boxes[8] && this.boxes[2] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[0] === this.boxes[4] && this.boxes[0] === this.boxes[8] && this.boxes[0] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes[2] === this.boxes[4] && this.boxes[2] === this.boxes[6] && this.boxes[2] !== "empty"){
        this.winMessage = `${this.boxes[0]} is Won`
      }
      else if(this.boxes.includes("empty") !== true){  
        this.reset()
        return Alert.fire("Match Draw ")
        
      }
    },
    showDialog(){
      Alert.fire({
        title: "Game Over",
        text: `${this.winMessage}`
      })
    }
  }
}
</script>

<style>
.outer{
  background-color: rgb(53, 52, 52);
  height: 100vh;
}
.grid{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 5px;
}
</style>