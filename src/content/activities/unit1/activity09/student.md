``` jv
function setup() {
  createCanvas(600, 400); 
  noStroke(); 
  background(0); 
}

function draw() {
 
  let x = random(width);
  let y = random(height);
  let size = random(10, 50);
  let colorR = map(sin(frameCount * 0.01), -1, 1, 0, 255);
  let colorG = map(cos(frameCount * 0.02), -1, 1, 0, 255);
  let colorB = map(sin(frameCount * 0.03), -1, 1, 0, 255);
  let alpha = random(100, 200); 
 
  fill(colorR, colorG, colorB, alpha);
  ellipse(x, y, size, size);

}

```
