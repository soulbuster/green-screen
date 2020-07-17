# green-screen
//code for HTML
<script src = "https://www.dukelearntoprogram.com/course1/common/js/image/SimpleImage.js"></script>
<html>
  <title>green screen converter</title>
  <body>
    <p><h1> Green Screen Converter</h1>
    <canvas id ="can1"></canvas>
    <canvas id ="can2"></canvas>
    <canvas id ="can3"></canvas>
     <input type = "file" multiple = "false" accept="image/*" id = "finput" onchange="foreground()">
    <input type = "file" multiple = "false" accept="image/*" id = "binput" onchange = "background()">
    <input type = "button" value = "convert" id = "cnvt" onclick="cromakey()">
    </p>
  </body>
</html>

//code for CSS

h1{
  position: -webkit-sticky; 
  position: sticky;
  text-align: center;
  top: 0;
  background-color: orange;
  border: 2px solid #4CAF50;
}
body{
background-color: #7FFFD4;
}
canvas{
  width : 432px;
  height : 300px;
  border : 1px solid #c3c3c3;
}

//code for JavaScript

var x;
var y;
function foreground(){
  var fimg = document.getElementById("can1");
  var input = document.getElementById("finput");
  x = new SimpleImage(input);
  x.drawTo(fimg);
}
function background(){
  var bimg = document.getElementById("can2");
  var input2 = document.getElementById("binput");
  y = new SimpleImage(input2);
  y.drawTo(bimg);
}
function cromakey(){
  var output = new SimpleImage(x.getWidth(),x.getHeight());
  var displayf = document.getElementById("can3");
  if(x == null || y== null){
    alert("file not uploaded");
  }
  for(var pixel of x.values()){
   if(pixel.getGreen() > pixel.getRed() + pixel.getBlue() ){
    var xc = pixel.getX();
     var yc = pixel.getY();
     var final = y.getPixel(xc,yc);
     output.setPixel(xc,yc,final);
   } 
    else
      output.setPixel(pixel.getX() , pixel.getY() ,pixel);
  }
  output.drawTo(displayf);
}
