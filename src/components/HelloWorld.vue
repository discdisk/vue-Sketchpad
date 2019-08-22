<template>
  <div id="skechPad">
    <h1>{{msg}}</h1>
    <div>
      <label style=" ">recognition service URL: </label>
      <input type="text" v-model=ImageProcessServer placeholder="http://localhost:5000/demotext" style="width: 50%; margin-bottom:5px;">
    </div>
    <div class="btnFunc">
      <button v-on:click ="clearCanvas">clear</button>
      <button id="ebtn" v-on:click ="eraser">eraser</button>
      <button v-on:click ="send">send</button>
    </div>
    <input v-model='paintSize' type="range" min="1" max="30" value=10 class="slider" id="myRange">
    <h2 v-if='recognitionSuccess'>The recognition result is {{ result }} .</h2>
    <h2 v-else>ERROR.</h2>
    <canvas id="mycanvas" v-on:mousedown="startDraw" v-on:mousemove="draw" v-on:mouseup="stopDraw" v-on:mouseleave="stopDraw" @touchstart.prevent="startDraw" @touchmove.prevent="drawTouch" width="400" height="400" style="background:green; border:1px solid #c3c3c3; margin:0 auto;">not supported!</canvas>
    <div style="height:100px"></div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data: function(){
    return {
      recognitionSuccess:true,
      result:'_',
      ImageProcessServer:"http://localhost:5000/demotext",
      isCanvasMouseDown:false,
      paintSize:10,
      usePen:true,
      paintColor:"black",
      penColor:"black",
      eraserColor:"white"}
  },
  methods:{
    log(e){
      console.log(e)
    },
    drawTouch(e){
      if(this.isCanvasMouseDown){
        var canvas = document.getElementById("mycanvas");
        var ctx = canvas.getContext('2d');
        ctx.beginPath();
        ctx.fillStyle = this.paintColor;
        ctx.arc(e.changedTouches[0].pageX-e.changedTouches[0].target.offsetLeft,e.changedTouches[0].pageY-e.changedTouches[0].target.offsetTop,this.paintSize,0,2*Math.PI);  //arc(x,y,r,start,stop)
        ctx.fill();
      }
    },
    send(){
      console.log(this.canvas.toDataURL())
      this.result='...'
      // fetch('http://localhost:5000/demotxt',{imgURI:this.canvas.toDataURL()})
      axios({
        method: 'post',
        url: this.ImageProcessServer,
        data: {imgURI:this.canvas.toDataURL()}
      }).then(response => (this.result = response["data"])).then(this.recognitionSuccess=true).catch(error => (this.recognitionSuccess=false))

      
    },
    eraser(){
      var eraserBtn=document.getElementById("ebtn")
      this.usePen=!this.usePen
      if (this.usePen) {
        this.paintColor=this.penColor
        eraserBtn.style.background = "palegreen";
      } else{
        this.paintColor=this.eraserColor
        eraserBtn.style.background = "oldlace";
      }
    },
    startDraw(){
      this.isCanvasMouseDown=true;
    },
    stopDraw(){
      this.isCanvasMouseDown=false;
    },
    draw(e){
      if(this.isCanvasMouseDown){
        this.ctx.beginPath();
        this.ctx.fillStyle = this.paintColor;
        this.ctx.arc(e.layerX,e.layerY,this.paintSize,0,2*Math.PI);  //arc(x,y,r,start,stop)
        this.ctx.fill();
      }
    },
    clearCanvas(){
      this.ctx.fillStyle = "white";
      this.ctx.rect(0,0,this.canvas.width,this.canvas.height);  //(x,y,width,height)
      this.ctx.fill();
    }

  },
  mounted () {
    this.canvas = document.getElementById("mycanvas");
    this.ctx = this.canvas.getContext('2d');
    this.clearCanvas()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#skechPad{
  margin:0 auto;
  width:400px;
}

.btnFunc{
  display: flex;
  display: -webkit-flex;
}

button {
  border:hidden;
  font-size: 30px;
  flex:1;
  -webkit-box-flex: 1;
  margin: 1px;
  background:palegreen;

}

.slider {
  
  margin: 1px;
  margin-top:10px;
  -webkit-appearance: none;
  width: 100%;
  height: 20px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  background: #4CAF50;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  background: #4CAF50;
  cursor: pointer;
}
</style>
