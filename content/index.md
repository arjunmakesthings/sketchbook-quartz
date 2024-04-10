***
### night code jams with S #punctual 
S was around and I excitedly showed her Punctual. We messed around with a few blocks of code, without letting logic govern us.

![[Screen Recording 2024-04-08 at 11.26.48 PM.mov]]
``` c
--bg
 
 
o << 0.4; 
 
r << 0.1; 
g << 0.2; 
b << 0.08;  
 
-- top square
move [osc(rnd)] $ 
spin [osc(0.02)] $ 
zoom [osc(0.080)] $ 
move [osc(fr*0.0002)] $  
tile [5,3] $ 
spin[osc(0.09)] $ 
circle [0,0] [2,2, 2] * o * hsvrgb[cam, r,g,b]>> video;

-- osc (62) >> audio; 
 
-- [0,0,0] >> video; 
```

*** 
![[Screen Recording 2024-04-08 at 11.20.11 PM.mov]]

``` c 
--bg
 
 
o << 0.4; 
 
r << 0.1; 
g << 0.02; 
b << 0.08;  
 
-- top square
zoom [osc(0.02)] $ 
move [osc(fr*0.0002)] $  
tile [3,3] $ 
spin[osc(0.2)] $ 
rect [0,0] [2,2, 2] * o * hsvh[r,g,b,cam]>> video;

-- osc (62) >> audio; 
 
-- [0,0,0] >> video; 

```

![[Screen Recording 2024-04-08 at 11.09.51 PM.mov]]

``` c
-- flower
[0,0,0] >> video; 
 
o << 0.6;  
 
x << 0; 
y << 0; 
d << 1;
 
rot << [0, 0.3 .. 1]; 
 
r << 0.87; 
g << 0.19; 
b << 0.38; 
 
 
zoom [2,2] $ 
fit (1/1) $ 
spin ([rot]) $ 
fit [0.5/2] $ 
circle [x,y] [d] * o * [cam] >> video; 

```

23:10, 2024-04-08

***
### it's just a wave and i know #p5 
Used the same text manipulations as earlier with mapping sine waves. Made while thinking of John Mayer's song. 

![[vid.mov]]

Love the treatment it produces. 

![[Screenshot 2024-04-04 at 5.25.35 PM.png]]

``` js
  for (let i = 0; i < xPos.length; i++) {
    //let wa = int(noise((i + waveOffset) / 70) * waveHeight);

    let wa = map(sin(i*waveOffset), -1,1, 0, 10); 
    let wave = wa*waveHeight; 

    let col2 = map(wave, -25, 25, 10, 40);

  fill (h,s,col2); 

    push();
    translate(xPos[i], yPos[i]+wave);
    ellipse (0,0,gridSize*3, gridSize+wave*1.2); 
    pop();

  waveOffset += yPos[i]*waveSpeed;
  }
```

17:27, 2024-04-04

***
### portrait maker #punctual 

![[Screenshot 2024-04-03 at 5.08.54 PM.png]]

``` c
-- flower

[0,0,0] >> video; 

o << 0.6;  

x << 0; 
y << 0; 
d << 0.8;

rot << [0, 0.3 .. 1]; 

r << 0.87; 
g << 0.19; 
b << 0.38; 


fit (1/1) $ 
spin ([rot]) $ 
fit [0.5/2] $ 
circle [x,y] [d] * o * rgbs[r,g,b] >> video; 
```

17:09, 2024-04-03

***
### cam flower #punctual 
Flower with video input. 

![[Screen Recording 2024-04-03 at 5.03.35 PM.mov]]

``` c
-- flower
[0,0,0] >> video; 

o << 0.6;  

x << 0; 
y << 0; 
d << 0.8;

rot << [0, 0.3 .. 1]; 

r << 0.87; 
g << 0.19; 
b << 0.38; 


fit (1/1) $ 
spin ([rot]) $ 
fit [0.5/2] $ 
circle [x,y] [d] * o * rgbs[r,g,b] >> video; 
```

17:05, 2024-04-03

***
### wip #punctual 
``` c
o << 0.6;  

rot << [0,0.2 .. 1.2];  

-- pink: https://htmlcolorcodes.com/colors/shades-of-pink/

r << 0.87; 
g << 0.19; 
b << 0.38; 

zoom [2,2] $ 
fit [1/1] $ 
spin [osc(rot*0.02)] $ 
fit [0.5/2] $ 
circle [0,0] [0.3] * o * rgbs[cam] >> video; 

```

*** 
### Rotating Flower #punctual 

![[Screen Recording 2024-04-02 at 4.53.48 PM.mov]]

16:54, 2024-04-02

``` c
o << 0.06;  

rot << [0,0.2 .. 1.2];  

-- pink: https://htmlcolorcodes.com/colors/shades-of-pink/

r << 0.87; 
g << 0.19; 
b << 0.38; 

fit [1/1] $ 
spin [osc(rot*0.02)] $ 
fit [0.5/2] $ 
circle [0,0] [0.3] * o * [r,g,b] >> video; 
```


![[Screenshot 2024-04-02 at 4.48.34 PM.png]]

``` c
o << 0.006;  

r << [0,0.2 .. 1.2];  

spin [osc(r*0.02)] $ 
fit [0.5/2] $ 
circle [0,0] [0.3] * o >> video; 
```

16:48, 2024-04-02

***
### petal #punctual 
Making a petal. No ellipse on Punctual so distorting a circle. 

``` c
o << 0.6;  

fit [0.5/2] $ 
circle [0,0] [0.3] * o >> video; 
```

16:40, 2024-04-02
***
### I'm Shattering But It Doesn't Matter #p5 
Lately been re-excited by the idea of using code for expressive typography. 

![[Screen Recording 2024-03-28 at 2.53.19 PM.mp4]]

![[Screenshot 2024-03-28 at 2.54.00 PM.png]]

``` js
//I'm Shattering But It Doesn't Matter


let xPos = [];
let yPos = [];
let gridSize = 5;

let waveOffset = 0; // Starting wave offset for animation
let waveSpeed = 1.2; // Adjust speed of wave movement
let waveHeight = 100; // Amplitude of the waves

let h = 211;
let s = 82;
let l = 24;

function setup() {
  createCanvas(1000, 1000);
  noStroke();
  colorMode(HSL);

  convertLetterToPoints();
}

function draw() {
  //background(h,s,l-40);
  background(0);

  fill(255);

  for (let i = 0; i < xPos.length; i++) {
    let wave = int(noise((i + waveOffset) / 70) * waveHeight);

    let col2 = map(wave, -25, 25, 30, 70);

    // fill(h, s, col2);

    //square(xPos[i]+random(-2,2)+wave, yPos[i]+random(-2,2), wave/4);

    push();
    translate(xPos[i], yPos[i] + wave);
    rotate(wave / 10);
    textSize(32);
    text(":)", 0, 0);
    pop();
  }

  waveOffset += waveSpeed;

  /*

  // Generate a wave pattern using sine function
  for (let y = 0; y <= height; y += 50) {
    let wave = sin((y + waveOffset) / 50) * waveHeight;
    fill(100 + wave, 150 + wave, 255); // Light blue water with wave height variation

    // Draw water based on y position and wave offset
    circle(500, y, 300+wave);
  }

  // Update wave offset for animation
  waveOffset += waveSpeed;

  */
}

function convertLetterToPoints() {
  textAlign(LEFT, CENTER);

  //TypeToPoint
  let points = [];

  background(255);

  fill(0);

  //Text Properties
  //textFont(font);

  var tSize = 170;
  textFont("IBM Plex Serif");
  textSize(tSize);
  textLeading(tSize);
  text(
    "i'm shattering but it doesn't matter", 60, -40, width / 2 + width / 2, height / 2 + height / 2
  );

  loadPixels();

  var change = 3;
  for (let y = 0; y < height; y += gridSize + change) {
    for (let x = 0; x < width; x += gridSize + change) {
      let px = get(x, y);
      let r = px[0];
      if (r < 200) {
        points.push(createVector(x, y));
      }
    }
  }
  for (let i = 0; i < points.length; i += 2) {
    let x = points[i].x;
    let y = points[i].y;

    xPos.push(x);
    yPos.push(y);
  }
}

```

15:04, 2024-03-28

***
### Won't you stand by me – typographic sketch #p5 
Wrote a sketch with particles that oscillate between two defined positions on the screen. 

![[vid1.mp4]]

![[Screenshot 2024-03-25 at 4.05.38 PM.png]]

![[Screenshot 2024-03-25 at 4.05.26 PM.png]]

![[Screenshot 2024-03-25 at 4.05.30 PM.png]]

Used sin(inc) to give a number between -1 and 1. To smooth out the animation, the inc is incremented by 0.02 every frame. 

``` js
  update() {
    this.x = map(sin(this.inc), -1, 1, this.x1, this.x2, true);
    this.y = map(sin(this.inc), -1, 1, this.y1, this.y2, true);

    this.s = map(sin(this.inc+this.inc), -1,1, gridSize*3, gridSize/2, true); 

    this.inc += 0.02;
  }
```

16:08, 2024-03-25

***
### Washed up potential – text as a water wave #p5
Wanted to treat text like a wave hitting the beach with many particles. First figured out what a wave would look like: 

``` js
  for (let y = 0; y <= height; y += 50) {
    let wave = sin((y + waveOffset) / 50) * waveHeight;
    fill(100 + wave, 150 + wave, 255);

    circle(500, y, 300+wave);
  }
  waveOffset += waveSpeed;
```

Then used my convertToText function to make the same happen for a piece of text: 

![[washed up potential.mov]]

``` js
//Washed Up Potential

let xPos = [];
let yPos = []; 
let gridSize = 5; 

let waveOffset = 50; // Starting wave offset for animation
let waveSpeed = 1.2; // Adjust speed of wave movement
let waveHeight = 30; // Amplitude of the waves

let h = 211; 
let s = 82; 
let l = 24; 

function setup() {
  createCanvas(1000, 1000);
  noStroke(); 
  colorMode (HSL); 

  convertLetterToPoints(); 
}

function draw() {
  //background(h,s,l-40); 
  background(h,s,l+73); 


for (let i = 0; i<xPos.length; i++){
  let wave = int(sin((i + waveOffset) / 50) * waveHeight);

  console.log(wave); 

  let col2 = map(wave, -25 ,25, 30, 70); 

  fill (h,s,col2); 

square (xPos[i]-wave/20, yPos[i], int(wave/1.8)); 
}

waveOffset += waveSpeed;

}

function convertLetterToPoints() {
  textAlign(LEFT, CENTER);

  //TypeToPoint
  let points = [];

  background(255);

  fill(0);

  //Text Properties
  //textFont(font);

  var tSize = 240; 
  textFont("Garamond");
  textSize(tSize);
  textLeading (tSize/1.2); 
  text('am i just washed up potential?', 60, -5, width/2+width/2, height/2+height/2);

  loadPixels();
  for (let y = 0; y < height; y += gridSize) {
    for (let x = 0; x < width; x += gridSize) {
      let px = get(x, y);
      let r = px[0];
      if (r < 200) {
        points.push(createVector(x, y));
      }
    }
  }
  for (let i = 0; i < points.length; i+=2) {
    let x = points[i].x;
    let y = points[i].y;

    xPos.push(x);
    yPos.push(y);
  }
}


```


![[Screenshot 2024-03-24 at 12.21.57 PM.png]]

12:27, 2024-03-24
***
### rotational studies #p5
Simple rotational studies based on yesterday's logic, but no animation. Used iteration through the array as variance. 


![[rotStudy.png]]

![[rotStudy4.png]]

![[rotStudy5.png]]

![[rotStudy6.png]]

16:27, 2024-03-22

***
### looping animations #p5 
Wanted to study how perfect loops could be made with simple shapes. Made something with squares, but still can't figure out the math for the sketch to make a loop, will have to do it on a video editor for now. 

``` js
//Rotate based on odd-even; March, 2024.
let margin = 50;
let s = 75;
let tiles = [];
function setup() {
  createCanvas(1000, 1000);
  rectMode(CENTER);
  noStroke();
  angleMode = DEGREES;
  for (let x = margin; x <= width - margin; x += s) {
    for (let y = margin; y <= height - margin; y += s) {
      tiles.push(new Tile(x, y));
    }
  }
}
function draw() {
  background(0);
  for (let i = 0; i < tiles.length; i++) {
    var r = 0;
    if (i % 2 == 0) {
      r = 45;
    } else {
      r = 90;
    }
    tiles[i].display(r);
  }
}
```

The class: 

``` js
class Tile {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.s = s;
    this.r = 0;
  }
  display(r) {
    push();
    translate(this.x, this.y);
    this.r = r;
    var t = frameCount / 60;
    this.rot = map(sin(this.r * t * 0.00003), -1, 1, 0, 360);
    fill(255);
    rotate(this.rot);
    square(0, 0, this.s);
    pop();
  }
}
```

The problem because of which it isn't perfectly looping via code is that I slow down rotation by multiplying values with 00003. Need to figure this out. 

![[loop.mp4]]

Ooh! Maybe I could use radians instead of degrees, maybe that value progression is better. 

16:09, 2024-03-21

***
### kucch crazy ho gaya #punctual 

![[Screenshot 2024-03-20 at 10.53.51 PM.png]]

``` c
--bg


o << 0.2; 

r << 0.1; 
g << 0.02; 
b << 0.08;  

-- top square 
spin[osc(cam*0.002)] $ 
rect [cam,0] [2,2] * o * [r,cam/2,cam/0.8]* o>> video;

[0,0,0] >> video; 
```


![[Screenshot 2024-03-20 at 10.55.02 PM.png]]

22:55, 2024-03-20
***
### face in rectangle #punctual 
Trying to clip face to make typography. I don't understand what's happening, but let's see. I'll figure it out. 

``` c
[0,0,0] >> video; 

o << 1; 

rect [0, 0] $ 
[cam] * o >> video; 
```

![[Screenshot 2024-03-20 at 10.32.19 PM.png]]

22:32, 2024-03-20
***
### in progress #punctual 

``` c
o << 0.8;

x << [-2, -1.9 .. 2]; 
y << 0; 

w << 0.2; 

-- [1,1,1] >> video; 

[0,0,0] >> video; 

r << 0.2; 
g << 0.8; 
b << 0.1; 

w << 0.02; 

spin [osc(pi*0.02)] $ fit (1/1) $ rect [x, y] [w,w] * o >> video; 
```

***
### repeating video input in the shape of a flower #punctual 
Repeat video input in the shape of a flower. 

``` c
-- video flower

z << 0.8; 

a << [0, 0.2 .. 1]; 

o << 0.3; 


r << 1; 
g << 0.31; 
b << 0.61; 

col << [r,g,b]*o;

z2 << 0.9;  

zoom [z2*(-1), z2] $ tile [2, 2] [[fit (1/1) $ spin [a] $ [zoom[(z*(-1)),z] [cam]]]]* o * [col]>> video; 
```

![[Screenshot 2024-03-17 at 10.21.41 PM.png]]

22:20, 2024-03-17
***
### making an 'a' with video input #punctual 
Made a lower-case 'a' with shaders on Punctual. 

``` haskell
-- creating an A

s << 0.1; 

x << [0, 0.1 .. 0.5]; 
y << [0]; 

o << 0.4; 

r << 0.1; 
g << [x]*0.08; 
b << 0.8; 


z << 0.18; 

spinVal << 0; 

-- bar 

spin [osc(spinVal)] [move [x,0.7] [zoom [(z*(-1)), z] (fit (0.02/0.02) $ cam) * o  *[r,g,b]]] >> video; 

-- center

midStem << [-0, -0.1 .. 0.85]; 

spin [ osc(spinVal)] [move [0.5,midStem] [zoom [(z*(-1)), 0.5] (fit (0.02/0.02) $ cam) * o *[r,g,b]]] >> video; 

-- bottom 

spin [ osc(spinVal)] [move [x,-0.5] [zoom [(z*(-1)), z] (fit (0.02/0.02) $ cam) * o *[r,g,b]]] >> video; 

spin [osc(spinVal)] [move [x,midStem+0.2] [zoom [(z*(-1)), 0.05] (fit (0.02/0.02) $ cam)* o *[r,g,b]]] >> video; 

spin [osc(spinVal)] [move [-0.0005,midStem-0.29] [zoom [(z*(-1)), 0.5] (fit (0.02/0.02) $ cam) * o  *[r,g,b]]] >> video; 
```

![[Screenshot 2024-03-16 at 9.00.53 PM.png]]

21:02, 2024-03-16
***
### make rows of video feed

``` c
z << 0.1; 
x << [0, 0.1 .. 0.5]; 

move [x,0] [zoom [(z*(-1)), z] (fit (0.02/0.02) $ cam)] >> video; 
```

***
### noisy background #punctual 
Grey, noisy background. 

``` c
0, 0, 0 >> video;

x << osc ([fx*0.2]*0.08);
y << osc ([fy*0.0002]*0.2);  

w << osc(fr*0.5)*0.7;
h << 1;

-- r << 0.5; 
-- g << 0.5; 
-- b << 0.5; 

rect [x, y] [w, h] *0.3 >> video;

---

0, 0, 0 >> video;

-----------------------
r << [0.1, osc (fx)*0.7, fr*0.2]; 
g << 0; 
b << [1, 0, 0.3]; 

x1 << osc [((fr*fy)), fr], fr; 
y1 << 0; 

w << [0.1, 0.2, 0.2]; 
h << [fy, fx, 2]; 

rect [x1,y1] [w, h] * [0.8] * [r,g,b] >> video; 
```

***
### ripple #punctual 
Makes a water ripple. 

``` haskell
0, 0, 0 >> video; 

w << fr/0.02; 

h << 2; 

v << (ft*0.02); 

spin [osc(fr*0.002)*sin(fx*0.0002)*cos(fx)] (move [osc(fx*0.000008), ft*4] (hline [v*0.002] [w*10, h] * 0.8 * [osc(fx*0.002),0.1*v, osc(v*0.3)])) >> video;
```

***
### water #punctual {{date}}
Simulates something of a water kind. 

```c
x << [0.3,0.2,0.3,0.8]; 

move[sin(fx+fy*(1/4*fr)*fr), 0] [circle [x, fy][1.4]*0.8 * [0.1, 0.2, 0.3]] >> video; 
```
  ***


