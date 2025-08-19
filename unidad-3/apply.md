# Unidad 3


## 🛠 Fase: Apply


### Primer codigo 

```py
let count
let state
let startT



function setup() {
  
  starTime = 20
  count = 0
  state = 'Config'
  

  
  
  createCanvas(400, 400);
  connectBtn = createButton("A");
  connectBtn.position(80, 300);
  
  
  connectBtn = createButton("B");
  connectBtn.position(350, 300);
  
  connectBtn = createButton("S");
  connectBtn.position(200, 300);
  
  connectBtn = createButton("T");
  connectBtn.position(200, 50);
  
 
 

}

function draw() 
{
  
  background(400);
  text(starTime,40,200)
  textSize(50)
  fill(0)
  
  
  if (state == 'Config')
  {
    if (starTime < 60 && starTime > 10 && connectBtn.mousePressed)
    {
      starTime++
    }
  }
  
}
```
