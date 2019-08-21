<template>
  <div>
    <h1>{{msg}}</h1>
    <div class="btnFunc">
      <button v-on:click ="clearCanvas">clear</button>
      <button id="ebtn" v-on:click ="eraser">eraser</button>
      <button v-on:click ="send">send</button>
    </div>
    <input v-on:change='sliderValue' type="range" min="1" max="30" value="10" class="slider" id="myRange">
    <p>The recognition result is {{ result }} .</p>
    <canvas id="mycanvas" v-on:mousedown="startDraw" v-on:mousemove="draw" v-on:mouseup="stopDraw" @touchstart.prevent="startDraw" @touchmove.prevent="drawTouch" width="400" height="400" style=" border:6px solid #c3c3c3;">not supported!</canvas>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data: function(){
    return {
      result:'_',
      isCanvasMouseDown:false,
      paintSize:10,
      usePen:true,
      paintColor:"#ccccff",
      penColor:"#ccccff",
      eraserColor:"white"}
  },
  methods:{
    log(e){
      console.log(e.changedTouches[0])
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
      var canvas = document.getElementById("mycanvas");
      console.log(canvas.toDataURL())
      
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
    sliderValue(e){
      this.paintSize=e.target.value
    },
    startDraw(){
      this.isCanvasMouseDown=true;
    },
    stopDraw(){
      this.isCanvasMouseDown=false;
    },
    draw(e){
      if(this.isCanvasMouseDown){
        var canvas = document.getElementById("mycanvas");
        var ctx = canvas.getContext('2d');
        ctx.beginPath();
        ctx.fillStyle = this.paintColor;
        ctx.arc(e.layerX,e.layerY,this.paintSize,0,2*Math.PI);  //arc(x,y,r,start,stop)
        ctx.fill();
      }
    },
    clearCanvas(){
      var canvas = document.getElementById("mycanvas");
      var myRange = document.getElementById("myRange");
      console.log(myRange)
      var ctx = canvas.getContext('2d');
      
      ctx.clearRect(0,0,canvas.width,canvas.height);  //(x,y,width,height)
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btnFunc{
  disply:flex;
}

button {
  border:hidden;
  flex:1;
  margin: 1px;
  width: 17%;
  background:palegreen;

}


.slider {
  -webkit-appearance: none;
  width: 50%;
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
