<template>
  <div id="app">
    <div class="window">
      <p class="text">найди одинаковые</p>
      <div class="first">
        <div v-for="(item, index) of blocks" :key="index">        
          <div :style="{background: item.back}" :class="{act: isActive}" class="block"  @click="correct(index); timerCount()" v-if="index<4">{{index+1}}</div>
        </div>      
      </div>
      <div class="second">
        <div v-for="(item, index) of blocks" :key="index">
           <div :style="{background: item.back}" :class="{act: isActive}" class="block"  @click="correct(index), timerCount()" v-if="index>3 & index<8">{{index+1}}</div> 
        </div>
      </div>
      <div class="third">
        <div v-for="(item, index) of blocks" :key="index">
          <div :style="{background: item.back}" :class="{act: isActive}" class="block"  @click="correct(index); timerCount()" v-if="index>7 & index<12">{{index+1}}</div>
        </div>        
      </div>
      <div class="fourth">
        <div v-for="(item, index) of blocks" :key="index">
          <div :style="{background: item.back}" :class="{act: isActive}" class="block"  @click="correct(index); timerCount()" v-if="index>11 & index<16">{{index+1}}</div>
        </div>        
      </div>  
      {{timer}}
      <div class="win">
        <div v-show="showWin">Вы выиграли!!!</div> 
      </div> 
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      count: 0,
      startTimer: 0,
      timer: "",
      isActive: false,
      colors: ["red", "blue", "orange", "purple", "green", "yellow", "brown", "pink"],
      blocks: [
      ],
      val:"",
      showWin: false
    }
  },
  mounted: function (){
    var count = 0;
    for (var i=0; i<this.colors.length; i++){
      var block = {};
      block.name = "block"+(count+1);
      block.color = this.colors[i]
      block.back = ""
      if(count<4){
        block.position = "first"
      }else if (count > 3 & count < 8){
        block.position = "second"
      }else if (count > 7 & count < 12){
        block.position = "third"
      } else if (count > 11  & count < 16){
        block.position = "fourth"
      }
      
      this.blocks.push(block)      
      count++
      var block1 = {};
      block1.name = "block"+(count+1);
      block1.color = this.colors[i]
      block1.back = ""
      
      if(count<4){
        block1.position = "first"
      }else if (count > 3 & count < 8){
        block1.position = "second"
      }else if (count > 7 & count < 12){
        block1.position = "third"
      } 
      this.blocks.push(block1)
      count++
    }
    function compareRandom(a, b) {
      return Math.random() - 0.5;
    }
    this.blocks.sort(compareRandom);
    
  },
  methods:{
    timerCount(){
      this.startTimer ++
      var min, sec, msec
      if(this.startTimer === 1){
        min=0
        sec=0
        msec=0;
        msec = msec + 1;
        this.timer = min+":"+sec+":"+msec
        //timer = setTimeout("timerCount()",10);
      } else {
        msec = msec + 1;
        this.timer = min+":"+sec+":"+msec
      }
      
    },
    correct(index){
      if(this.val===""){
        this.blocks[index].back = this.blocks[index].color
        this.val = index
      } else {
        if (this.blocks[this.val].color === this.blocks[index].color){
          this.blocks[index].back = this.blocks[index].color
          this.count++;
          this.val = ""

        } else {
          this.blocks[index].back = this.blocks[index].color
          this.isActive = true;
          var self = this;
          set = setTimeout(function () {
            self.blocks[index].back = ""
            self.blocks[self.val].back = ""
            self.val = ""
            self.isActive = false
          }, 1000);
        }
        this.val1 = ""
      }
      if (this.count === 8){
        this.showWin = true
      }
      
    },
    
    
  },
  computed:{
    
  }
}
</script>

<style>
  html,body{
    width: 100%;
    height: 100%;
  }
  #app{
    position: absolute;
    width: 100%;
    height: 100%;
    background: #AD66D5;
  }
  .window{
    position: absolute;
    width: 290px;
    margin: 20px 0 0 -150px;
    left: 50%; 
    border: 1px solid black;
    border-radius: 10px;
    padding: 10px;
    background: #876ED7;
  }
  .block{
    width: 50px;
    height: 50px;
    margin: 10px;
    border: 1px solid black;
    box-shadow: 0px 0px 2px 2px #424242;
  }
  .first{
    position: absolute;
    margin: 0px 0 0 10px
  }
  .second{
    position: absolute;
    margin: 0px 0 0 70px
  }
  .third{
    position: absolute;
    margin:0px 0 0 130px
  }
  .fourth{
    position: absolute;
    margin:0px 0 0 190px
  }
  .act{
    pointer-events: none;
  }
  .text{
    text-align: center;
    font-size: 25px;
    text-transform: uppercase;
    font-weight: bold;
    font-style: italic;
    font-variant: small-caps;
  }
  .win{
    text-align: center;
    color: red;
    font-size: 30px;
    font-weight: bold;
    margin:  270px 0 0 0;
  }
</style>
