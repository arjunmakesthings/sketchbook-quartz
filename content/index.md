***
### drawings with the cartesian coordinate system #p5 
i have been toying around the idea of using the cartesian coordinate system as a framework to generate drawings. 

![[Screenshot 2024-10-11 at 7.53.58 PM.png]]

some outputs from 11th october:

![[2.jpeg]]

![[3.jpeg]]

i think this sets the base for a long-term project, perhaps something that i can explore over the course of months. it also improves my understanding of drawing with 2D geometry.

outputs will get increasingly complex with time. 

![[4.jpeg]]

19:55, 2024-10-11

***
### lift pattern #p5 

![[lift_pattern_loop.mov]]

saw the original (static) pattern on the roof of sakina's lift. an ellipse is overlaid with a rotating square. messing around with radii leads to scope of exploration with figure & ground. 

``` js
//Sakina's Lift; October, 2024. 
let r = 50; 
let margin = r; 

function setup() {
    createCanvas(1000, 1000);
    rectMode(CENTER); 
    angleMode (DEGREES); 
    noStroke(); 
  }
  
  function draw() {
    background(0);

    var t = frameCount/60; 

    for (let x = margin; x<=width-margin; x+=r){
      for (let y = margin; y<=height-margin; y+=r){
      fill (255); 
      ellipse (x, y, r); 

      push(); 
      translate (x,y); 

      //debug
      /*
      rotate (45); 
      fill ('red'); 
      */

      //actual
      fill (0); 
      rotate (sin(t)*500); 

      square (0,0,r/1.3, r/10); 
      pop(); 
      }
    }
  }
```

21:02, 2024-10-08

***
### maybe i need to make it static #p5 
if it runs in real time, it lags quite a bit. anyway, made progress on the new painter. 

![[Screenshot 2024-09-30 at 2.34.29 PM.png]]

parameters: 

``` js
      /*
      PARAMETERS

      //brush selection
      - brushWidth = how thick the end-stroke is supposed to be. think of it like paintbrush 'size' (breadth).
      - frayness = how far apart (vertically) are the bristles from each other? 
      - fineness = how far apart (horizontally) are the bristles from each other?
      - bristleWidth = how thick are the bristles themselves?

      //colour
      - colour = what (all) colours do you want in your painting?
      - opacity = how opaque or transparent do you want your strokes to be?

      //starting position
      - margin = set the margin for your composition.
      - originX, originY = starting x and y position on the canvas.
      - startingAngle = at what angle do you place your paintbrush.

      //travel
      - directionToMove = what direction are you going to move your brush in?
      - distance = what distance should the paintbrush travel?
      - pace = how fast should the paintbrush travel?
      */

```

14:37, 2024-09-30

***
### new painting algorithm #p5 
i revisited my old computer-painting algorithm. 

![[Screenshot 2024-09-29 at 11.08.20 PM.png]]

![[Screenshot 2024-09-29 at 11.10.10 PM.png]]

![[Screenshot 2024-09-29 at 11.02.42 PM.png]]

![[Screen Recording 2024-09-29 at 11.07.56 PM.mov]]

since my understanding of programming has become better, i was able to rethink the algorithm. now, each brushStroke is treated as an object that gets the following data as input: 

``` js
    //A brushStroke has a starting position (originX, originY), brushWidth (the breadth of the stroke), startingAngle, distance (that it has to travel), pace (speed at which it is supposed to travel), colour & opacity of that colour, how much the bristles have frayed (frayness), fineness (how close or apart the bristles are from each other) and bristleWidth (how small or big are the bristles). 

constructor(originX, originY, brushWidth, startingAngle, distance, pace, colour, opacity, frayness, fineness, bristleWidth, directionProbability){

}

```

23:13, 2024-09-29

***
### everything is about u
p5 sketch. 

![[everything is about u.mov]]

Used the shape of a parabola to represent 'u'. Wanted a trail system but couldn't figure it out; so gave variance by changing size. 

``` js
 var seconds = frameCount / 60;

    //yStretch=map(noise(seconds), 0, 1, 10, 50);

    this.x = map(sin(seconds), -1, 1, -xStretch, xStretch);
    this.y = map(this.x * this.x * 6, 0, xStretch * xStretch, 0, yStretch);

    this.s = map(noise(seconds), 0, 1, 3, 20);

    //circle(initX + x, initY - y , 50);

    circle(this.initX + this.x, this.initY - this.y, this.s);

```

The formula for a (reverse) parabola is this: 

``` js
  var seconds = frameCount / 60;

  var x = map(sin(seconds), -1, 1, -xStretch, xStretch);

  //quadratic equation to give parabola y = x*x
  var y = map((x*x)*1, 0, xStretch*xStretch, 0, yStretch); 

  circle(initX + x, initY - y , 50); 
  
```

Also, fixed my lettersToPoints library to include maxWidth and maxHeight as well. And now it's deliverable via CDN: https://github.com/arjunmakesthings/p5.textToPoints

17:28, 2024-09-22

***
### this is how i feel #p5 + #strudel 
visuals and music. 

visuals inspired by the thought – we're two bodies in space. music inspired by gravity, john mayer. i miss you. 

![[Screen Recording 2024-09-21 at 11.26.27 PM.mov]]

``` js
//we're two bodies in space, september 2024.

$: s ("[[hh , [bd]] hh hh [hh , sd] hh hh] , <oh>/4").cpm(23).bank("ViscoSpaceDrum").room("0 0.2")

$: n("<[0@ 1 3 5@] ~ [5@ 3 1 0@] ~> ").scale("G:major").sound("gm_electric_guitar_clean").cpm(23).room("0 0.2 1")

$: n ("0 , 0").sound("gm_fx_echoes").loopAt( "0.4 , 0.7").gain("0.2 ").lpf(500).room("0 0.2 0.4")

```


``` js
//sketching; squares and sine; september 2024.

let margin = 200;
let w = 800;
let h = 25; 

let amp = 70;

function setup() {
  createCanvas(1000, 1000);
  noStroke();
  rectMode(CENTER); 
}

function draw() {
  //background('#176383');
  background(0);

  var t = frameCount / 60;

  fill(255);
  //noFill(); 

  for (let x = margin; x <= width - margin; x += w/2) {
    for (let y = margin; y <= height - margin; y += h) {
      push(); 
      translate (x + sin(y + t) * amp, y); 
      //var ang = map(sin(t), -1, 1, 0, TWO_PI); 
      var ang = (t+sin(y+t))*0.2
      rotate (ang)
      rect(0, 0, w*(sin(y+t)*0.4), h);
      pop(); 
    }
  }
}
```

23:29, 2024-09-21
***
### strudel + learning hydra #strudel #hydra #livecoding

i like the idea of 'livecoding'. someday, perhaps, i can perform for people. 

i enjoyed reading a little bit about hydra. i think there's a lot of potential there. will deep-dive. 

![[perf3.mov]]

``` js

//21 Sep, 2024.

await initHydra()
osc(10 , 0.09 , (Math.PI*2)*0.1).kaleid(Math.PI*2).scale(1,1,()=>window.innerWidth/window.innerHeight).out()


$: n("[<3 [5 7] [3@] 1>*2] , <<[4]*2> <[5]*2> <[7]*2> <[3]*2>>").scale("A2:minor, C3:major").sound("gm_slap_bass_2").gain ("0.7 , [0.3 0.6 0.9]")

$: s ("[hh]*12 [oh , bd]").delay("0 0.6 , 0").gain("0.1 [0.3 , 0.1]").bank("RolandCompurhythm1000 , EmuSP12").lpf("[500 1000 1500 2000] 5000")

$: note("<[f5]*3 [e4]*3 [d3]*3 ~ >*2 , <c2@ b2 a2 c2@>*2").sound("gm_drawbar_organ").lpf("8000")

```

17:34, 2024-09-21

***
### circles and sine #p5 

![[Screen Recording 2024-09-20 at 8.35.06 PM.mov]]

``` js
//sketching; circles and sine; september 2024.

let w = 50;
let margin = 0;

let amp = 200;

function setup() {
  createCanvas(1000, 1000);
  noStroke();
}

function draw() {
  //background('#176383');
  background(255);

  var t = frameCount / 60;

  //fill(255);

  for (let x = margin; x <= width - margin; x += 300) {
    for (let y = margin; y <= height - margin; y += w / 2) {

      fill (62, 210+(sin(y+t))*10, 198)
      circle(x + sin(x + y + t) * amp, y, w + sin(y + t) * 100);
    }
  }
}
```

20:37, 2024-09-20

***
### 20 sept - rainy day #strudel 

![[perf2.mov]]

``` js
//20 sept, rainy day

$: s ("<hh [hh hh hh] hh [hh hh hh] hh [hh hh hh] hh hh>*4").gain ("[0.1 1 0.1] 0.5")

$: s ("<oh - [oh oh] - >*2").gain("0.6")

$: s ("bd [bd - bd]*2").bank("BossDR110").amp("0.5"). gain("0.09 0.5")

$: note ("<[c]*2 [f g e a] [d]*2>").sound("gm_electric_guitar_jazz").gain ("[0.5 0.7 0.3] 0.4")

$: note ("<c c f g>").sound("gm_epiano1").echo(3, 1/6, .4).gain(0.4)
```

01:35, 2024-09-20

***
### finally a livecoding tool that works for me! #strudel
Discovered strudel during a computational arts festival here in Delhi. Love the software. Plus it's javascript; wondering how to combine p5 and strudel for some audio-visual stuff. 

I swear I had a sicker beat.

![[strudel1.mov]]

``` js
//cfgd melody

$: s("oh sd , bd -").delay ("0.3 0 ").amp("2 0").hush()

$: note ("[[c]*4 [f]*4 [g]*4 [d]*4]").sound("gm_synth_strings_2").amp ("0.8").lpf("1000")

$: s("<hh hh [hh hh] hh - sd ->*8").amp ("1").hush()

//$: s("[[hh]*16], [sd - sd oh], [bd - bd]*2").amp("0.01")

```

18:28, 2024-09-17

***
### make visual artefacts of digital rants #p5 
You can rant openly, without anyone else ever making full sense of what you said that day. I think this could be an interesting tool. 

I need to debug overlaps, add dates and the ability for people to save pictures of their rants.

![[Screenshot 2024-08-22 at 10.51.08 PM.png]]

![[vid 1.mov]]

![[Screenshot 2024-08-22 at 10.49.48 PM.png]]

22:53, 2024-08-22
*** 
### physics typography #p5 #matterjs

![[physics type crumble .mov]]

Based on my matterjs boilerplate, I used some elements of my previous writing tool work. 

You type, and create a 'sentence'. 

``` js
function keyTyped() {
  if ((keyCode != ENTER) & (key != " ")) {
    typedSentence += key;

    //actual display of letters
    /*
    xoff+=0.001; 
    xPos += textWidth(key)*random(2, 3, 5);
    ang += noise(xoff);

    letters.push(new Letter(key, xPos, yPos, ang));
    */
  } else if ((key == " ") | (key == ENTER)) {
    sentences.push(
      new Sentence(
        typedSentence,
        random(
          width / 2 - textWidth(typedSentence),
          width / 2 + textWidth(typedSentence)
        ),
        yPos
      )
    );
    //xPos += textWidth('OO') * 10;
    typedSentence = "";
  }
}

```

The sentence is a 'body'. 

``` js
class Sentence {
  constructor(t, x, y) {
    this.t = t;
    this.x = x;
    this.y = y;

    // Adjust density and remove slop
    this.body = Bodies.rectangle(
      this.x, 
      this.y, 
      textWidth(this.t) * 1.82, 
      tSize * 1.2, 
      {
        friction: 1,           // High friction to reduce sliding
        restitution: 0.0005,        // No bouncing
        mass: 0,        // Adjust density to reduce overlap
        inertia: Infinity,     // Prevent rotation
        frictionAir: 0.005      // Slight air resistance to slow down
      }
    );
    Composite.add(engine.world, this.body); 
  }

  display() {
    fill(255);
    textSize(tSize);

    textFont ("Crimson Pro"); 

    push();
    translate(this.body.position.x, this.body.position.y);

    // Debug: Show the bounding box
    fill(255);
    strokeWeight (1); 
    stroke (0); 
    rect(0, 0, textWidth(this.t) * 1.82, tSize * 1.2);

    // Display the text
    fill(0);
    noStroke(); 
    text(this.t, 0, 0);
    pop();
  }
}


```

I think I need to look at why the bodies aren't solid enough. They seem to overlap after some time. Is the density not enough? Maybe that could be set to infinity. Crap, forgot that. 

I think there's literal 'weight' in words. And a tool that allows you to write but also feel the weight in your words could be interesting. Maybe different words could have different 'weights'? 

I don't know. Still exploring. 

23:30, 2024-08-19

***
### matter.js boilerplate #p5 #matterjs 
Made this to never watch a video again to learn the fundamentals of matter.js. Further reference is here: https://brm.io/matter-js/docs/classes/World.html

``` js
//Boilerplate for getting started with matter.js; Arjun, August 2024. 

//Ensure you've added the matter.js file to your index.html file. 

//Most libraries are namespaced to avoid clashes with other language-specific variables. We create variables to avoid using matter.something every single time. 
var Engine = Matter.Engine,
    //Render = Matter.Render, //matter.js has an in-built renderer as well. However, since we're using p5, this isn't necessary for us. 
    Runner = Matter.Runner,
    Bodies = Matter.Bodies,
    Composite = Matter.Composite;

//global variables that will be used later:
var engine; 
var runner; 

//this is where you can declare your 'bodies' for later:
var particle; 

//this is for the ground: 
var ground; 

function setup() {
  createCanvas(windowWidth, windowHeight);

  //physics engine takes rect from center, center; so doing the same for p5
  rectMode (CENTER); 

  // Matter is a physics engine. So, we create an engine in the program: 
  engine = Engine.create(); 

  // This is where we can create bodies. Any initialisations of arrays can also go here. 
  particle = Bodies.rectangle (width/2, 0, 100,100); 

  // This is where we're creating a ground
  ground = Bodies.rectangle(width/2, height/2, 200, 20, {isStatic: true}); 

  // All bodies are composited, along with adding them to a 'world'. 
  Composite.add(engine.world, [particle, ground]); 

  // A runner keeps updating the engine and syncs it with the browser frame-rate. 
  runner = Runner.create(); 
  Runner.run(runner,engine); 
}

function draw() {

  background(0);

  // Bodies have inherent properties that are namespaced. We can use this to draw things. 
rect (particle.position.x, particle.position.y, 100,100);

//also drawing the ground for reference: 
fill (170); 
rect(width/2, height/2, 200, 20); 

}

```

22:09, 2024-08-19

***
### writing tool v1 #p5 
I'm working on a journalling tool of sorts? The goal is to try and help people capture a visual memoir of an automatic writing session. I think I'll work on this slowly, solving problems and exploring the scope through multiple versions. 

Today it was just about cracking the idea of typing on the screen and the letters being processed as individual shapes (so that I can perhaps try and manipulate them in some way). 

![[writing tool v1.mov]]

``` js
function keyTyped() {
  if (keyCode != ENTER) {

    // automatic line break
    if (xPos > width - 100) {
      yPos += tSize * 2; //consider this leading; at the moment double of text size.
      xPos = 100;
    }

    //actual display of letters
    xoff++; 
    xPos += textWidth(key)*random(2, 3, 5);
    ang += noise(xoff);

    letters.push(new Letter(key, xPos, yPos, ang));

  } else if (key == " ") {
    xPos += textWidth(O) * 3;
  }

      // forced line break
      if (keyCode == ENTER) {
        yPos += tSize * 2.5; //consider this after-para
        xPos = 100;
      }
}

```

00:51, 2024-08-18

***
### gaze-tracking prototype #p5 
finished working on an open-source gaze-tracking research tool prototype. 

code here: https://github.com/arjunmakesthings/gaze-tracker
use here: https://arjunmakesthings.github.io/gaze-tracker/index.html

maybe i have the potential to make more micro-tools and share them with the world; some silly, some, just perhaps, useful.

![[gaze-tracker.mp4]]

02:51, 2024-08-11

***
### webgaze #p5 
Figuring out gaze tracking via the webgaze.js library. Using a sketch by CedHon. 

![[Screen Recording 2024-07-28 at 11.58.58 PM.mov]]

I think it could be interesting to see if open source, accessible gaze-tracking tools could be made for UX research. 

I just need to figure out easier ways to train it, move it out of the training zone, track eye-movement data, and then present a summary of the findings. Time for a mini-program maybe? 

Too sleepy to do this right now. But yes, in the works. 

00:02, 2024-07-29
***
### i'm losing myself #p5 
Type sketch. Would be nice to sync it to a piano melody. Maybe I should create one using the same mathematical expressions? That could be interesting. 

![[i'm losing myself.mov]]


``` js
//I'm Losing Myself, June 2024.

let message =
  "i'm losing myself";

let horSpacing = 1;

let margin = 100;

let tSize = 12;

function setup() {
  createCanvas(800, 800);
  textAlign(CENTER, CENTER);
  rectMode(CENTER);
  textSize(tSize);
  fill(0);

  angleMode(DEGREES);
}

function draw() {
  background(255);

  var t = frameCount / 60;

  translate(width / 2, height / 2); 

  for (let i= 0; i<message.length; i++){
    noStroke(); 
    var a = 10; 
    var x = 300-i*40; 
    var y = i*8; 
    var ySpeed = (sin(t*i*4)); 
    var xSpeed = sin(t*10); 
    text(message, x*xSpeed, y*ySpeed);

    a+=200; 

    strokeWeight (0.5); 
    stroke (100); 
    line (x, y, x*xSpeed, y*ySpeed); 
  }
}

function mousePressed() {
  //save("frame.jpeg");
}

```

13:32, 2024-07-03

***
### first ever script #p5 
Published a [script](https://github.com/arjunmakesthings/textToPoints) to help people draw with text. It uses a resolved version of what Navya originally shared with me during a collaborative experiment, made a lot easier for anyone to plug & play. 

All the documentation is on [GitHub](https://github.com/arjunmakesthings/textToPoints). 

![[Screen Recording 2024-06-28 at 7.37.49 PM.mov]]

19:46, 2024-06-28
***
### growing up is messy #p5 
Type sketch. Made while mum was in surgery and I was writing my 'growing up' article. 

![[growing up 10s.mov]]

``` js

    for (let y = 20; y<=height-20; y+=50){
        for (let x = 20; x<=width-20; x+=230){
          for (let i = 0; i<t.length; i++){
            textSize (140+tSize); 
            tSize =  sin(frameCount*0.03)*100; 
            text (t[i], x+(i*20), y)
          }
        }
      }
```

12:20, 2024-06-27

***
### gravity-based #SonicPi 
Added a melody on top of the existing drum beat. Melody structure was simple, took notes from the Gravity intro and made SonicPi choose from the array. 

![[gravityJM_13June.wav]]

Fun melody structure. 

``` ruby
#Melody2
notes = [:E, :G, :G, :A, :A]

#use_random_seed 1010892

live_loop :melody , sync: :met do
  
  #use_synth_defaults attack: 0.5, decay 0.5,
  
  5.times do
    use_synth :piano
    play notes.choose
    sleep 1
  end
  
  sleep 6
  
  notes2 = [:E5, :G5, :G5, :A5, :A5]
  
  7.times do
    use_synth :piano
    play notes2.choose
    sleep 0.5
  end
  
  sleep 6
end
```

22:00, 2024-06-13

***
### gravity-inspired #SonicPi 
Was inspired by the structure of 'Gravity' by John Mayer. Attempted to recreate logically on SonicPi. 

The track has a high-hat that runs every beat. 

``` ruby
#inspired by Gravity

use_bpm 124

sample :drum_splash_hard

#Making a metronome
live_loop :met do
  sleep 1
end

#Setting ticker pattern
define :pattern do |pattern|
  return pattern.ring.tick === 'x'
end

live_loop :hh, sync: :met do
  sample :drum_cymbal_closed if pattern "xxxxxx"
  sleep 1
end
```

Then, there's the snare and the double kick-drum. 

``` ruby
#Drums
live_loop :kickDrum , sync: :met do
  with_fx :echo , decay: 0.08 , phase: 0.15 do
    sample :drum_heavy_kick , amp: 0.7 if pattern "x-----"
    sleep 1
  end
end

live_loop :snare , sync: :met do
  sample :drum_snare_hard if pattern "---x--"
  sleep 1
end
```

Essentially sounding like this: 
![[gravityDrumsOnly.wav]]

Then came the tricky part that I'm yet to figure out: the melody. For now, it's the chords with an ugly-sounding dpulse synth. 

``` ruby
#melody

melody_pattern = "-----------x------------"

notes = [:E, :G, :G, :A, :A]

live_loop :notes1, sync: :met do
  use_synth :dpulse
  
  if melody_pattern.look == "x" # Use look to check the current step in the pattern
    play :E
    sleep 1
    play :G
    sleep 0.5
    play :G
    sleep 1
    play :A
    sleep 1
    play :A , decay: 1
    sleep 1
    # No need for an else statement, just tick at the end
    tick # Move to the next step in the pattern
  else
    sleep 1
    tick # Move to the next step in the pattern even if not playing
  end
end

melody_pattern2 = "----------------------x"

live_loop :notes2, sync: :met do
  use_synth :dpulse
  
  if melody_pattern2.look == "x" # Use look to check the current step in the pattern
    play :E
    sleep 1
    play :G
    sleep 0.5
    play :G
    sleep 1
    play :A
    sleep 0.5
    play :A
    sleep 0.5
    play :A , decay: 1
    sleep 1
    # No need for an else statement, just tick at the end
    tick # Move to the next step in the pattern
  else
    sleep 1
    tick # Move to the next step in the pattern even if not playing
  end
end
```

Together sounding like this: 
![[gravityMelody_Trial1.wav]]

I think instead of chasing after Gravity, I can now start to play around with the structure that is created. Let's see what comes of it, might scrap the whole melody bit. It ain't working. 

12:42, 2024-06-12

***
### city grid #punctual 
Was meaning to try some text manipulation but ended up making a zooming in / out of a city grid like structure with some noise.

![[city grid.mov]]


``` ruby
a << 0.1; 

zoom [osc(0.005)] $ 
tile [1, osc(frt*0.2)*20] $ 
circle [0, 0] [10] * img "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSt6AfgR9v6HaWpAYVjMgHiYGmKYTwo136uyg&s" * 0.4
>> video; 
```

20:10, 2024-06-11

***
### even breathing is exhausting #p5 
Worked peacefully to try and understand how text is being processed, so that I can draw more effectively while maintaining the message. Made a simple sketch. 

![[even breathing is exhausting.mov]]

``` js
//Full code

//evenBreathingisExhausting, May 2024.

let message = "even breathing is exhausting";

let angle = 0;
let radius = 90;

function setup() {
  createCanvas(800, 800);
  background(255); //set background before sketch starts
  textAlign(CENTER, CENTER);
  textSize(14);
  fill(0);
  
  angleMode(DEGREES); //Radians to degrees
}

function draw() {
  background(255);

  for (let i = 0; i < message.length; i++) {
    let angle = ((TWO_PI * message.length * i) / message.length) * 2; //change i divisor to reduce gap between letters

    let x = width / 2 + cos(angle) * radius;
    let y = height / 2 + sin(angle) * radius;

    push();
    translate(x, y);
    rotate(map(i, 0, message.length, 0, 360));
    text(message[i], 0, 0);
    pop();
    radius += sin(frameCount) / 25; //increase divisor to make it smaller
  }
}

function mousePressed() {
  //save("frame.jpeg");
}

```

22:11, 2024-05-24

***
### more text #p5 

![[Screen Recording 2024-05-24 at 5.05.49 PM.mov]]

``` js
  for (let i = 0; i < message.length; i++) {
    for (let r = 20; r<=400; r+=5){
    let angle = (TWO_PI * message.length) * i;

    let x = width / 2 + cos(r+angle3) * r/2;
    let y = height / 2 + sin(r+angle) * 300;

    push();
    translate(x, y);
    //rotate(angle);
    text(message[i], 0, 0);
    pop();

    //radius+=0.04;

    angle3 +=0.0008;
  }
}
```

17:08, 2024-05-24

***
### text spiral #p5 

![[Screen Recording 2024-05-24 at 4.55.04 PM.mov]]

``` js
  for (let i = 0; i < message.length; i++) {
    for (let r = 20; r<=400; r+=15){
    let angle = (TWO_PI * message.length) * i*20;

    let x = width / 2 + cos(r+angle3) * i;
    let y = height / 2 + sin(angle) * r;

    push();
    translate(x, y);
    //rotate(angle);
    text(message[i], 0, 0);
    pop();

    //radius+=0.04;

    angle3 +=0.008;
  }
}
```

16:56, 2024-05-24

***
### more text stuff #p5 
I think the effect is pretty cool but it loses readability. But is that even important? Can't this just be a piece made from the aesthetics of letters? 

![[letters.jpeg]]

In all fairness, I have zero idea about what's happening in the code. I was just fiddling around with previous algorithms. But here: 

``` js
  for (let r = 20; r<=800; r+=8){
  for (let i = 0; i < message.length; i++) {
    let angle = (TWO_PI * message.length) * i*20;

    let x = width / 2 + cos(r+angle) * r;
    let y = height / 2 + sin(angle) * r;

    push();
    translate(x, y);
    //rotate(angle);
    text(message[i], 0, 0);
    pop();
    }
    }

```

It can also move apparently (?) 

![[Screen Recording 2024-05-24 at 4.51.51 PM.mov]]

16:52, 2024-05-24

***
### using beatbox-samples #SonicPi 
Messed around with some beatbox samples from the internet for some quick exploration. 

![[beatBox1.wav]]

``` ruby
use_bpm 120

#Making a metronome
live_loop :met do
  sleep 1
end

#Setting ticker pattern
define :pattern do |pattern|
  return pattern.ring.tick === 'x'
end
"
Custom loaded samples here

"

live_loop :kick, sync: :met do
  sample k, amp: 3 if pattern 'x-x-x-x-'
  sleep 0.5
end

live_loop :snare, sync: :met do
  sample s, amp: 3 if pattern '-x--xx-xx-x-x--'
  sleep 0.25
end

live_loop :sh, sync: :met do
  sample whisp, amp: 5 if pattern '-------x'
  sleep 0.5
end

"
live_loop :snare2, sync: :met do
  sample snare if pattern '---xx--xx'
  sleep 0.25
end
"

```


***
### we keep going around in spirals #p5 
Similar idea as the one before, doing drawing manipulations with each letter of a sentence. 

![[frame2.jpeg]]

![[Screen Recording 2024-05-23 at 6.00.14 PM.mov]]

``` javascript
  angleMode(DEGREES);

  let angle = 0;
  let radius = 0;

  for (let i = 0; i < message.length; i++) {
    let x = width / 2 + cos(angle) * radius;
    let y = height / 2 + sin(angle) * radius;

    push();
    translate(x, y);
    rotate(angle);
    text(message[i], 0, 0);
    pop();

    angle += baseAngleStep;
    radius += baseRadiusStep;
    baseAngleStep += 0.1;
    baseRadiusStep += 0.03;
  }
```

14:22, 2024-05-23

***
### text-recursion #p5 
Played around with the idea of making typography through recursion. 

![[Screen Recording 2024-05-22 at 2.52.27 PM.mov]]

First, I figured out a way to go through the "array" of a sentence. For example, if the sentence is: 

``` js
let message = "i'm so messed up";

for (let i = 0; i < message.length; i++) {
//Treats each character as an object – so you can do drawing manipulations. 
}
```

Then, I used some nested loops which I've been studying in the Stanford Code in Place course. 

``` javascript
function draw() {
  background(255);
  for (let x = 50; x <= width; x += 200) {
    for (let y = 0; y < height-90; y += 50) {
      for (let i = 0; i < message.length; i++) {
        push(); 
        translate (x + i * 9, 400+sin(y)*(i*100)); 
        rotate(sin(i*angle)*200);
        text(message[i], 0,0 );
        angle+=0.0003; 
        pop(); 
      }
    }
  }
}
```

14:55, 2024-05-22

***
### sonic-pi learning jam, 21 may #SonicPi
Boilerplate like DJ_Dave (https://www.youtube.com/watch?v=vuSZQnkOB_Y&t=389s) to set a metronome and ticker pattern. 

``` ruby
use_bpm 60

#Making a metronome
live_loop :met do
  sleep 1
end

#Setting ticker pattern
define :pattern do |pattern|
  return pattern.ring.tick === 'x'
end
```

Using patterns:

``` ruby
use_bpm 120

#Making a metronome
live_loop :met do
  sleep 1
end

#Setting ticker pattern
define :pattern do |pattern|
  return pattern.ring.tick === 'x'
end

live_loop :kickDrum, sync: :met do
  sample :bd_ada, amp: 1 if pattern "x--xxx--x----xx-"
  sleep 0.25
end

live_loop :hh, sync: :met do
  sample :drum_cymbal_closed if pattern "xxxx--xx--xxxx--"
  sleep 0.25
end
```

Basically, everything with "-" is a break. So, "xxxxxxxxxxxxxxxx" is the same as playing a loop with a certain amount of sleep between sounds. 

Made this with the above-mentioned logic: 

![[21May_Jam.wav]]

Here's the code: 

``` ruby
use_bpm 120

#Making a metronome
live_loop :met do
  sleep 1
end

#Setting ticker pattern
define :pattern do |pattern|
  return pattern.ring.tick === 'x'
end

live_loop :kickDrum, sync: :met do
  sample :bd_ada, amp: 1 if pattern "x--xxx--x----xx-"
  sleep 0.25
end

live_loop :hh, sync: :met do
  sample :drum_cymbal_closed if pattern "xxxx--xx--xxxx--"
  sleep 0.25
end

live_loop :vinyl, onset: 3, sustain: -2, decay: -2, sync: :met do
  sample :vinyl_scratch, amp: 0.2 if pattern "---------------x"
  sleep 1
end

#Piano
notes = (ring :E4, :Fs4, :B4, :Cs5, :D5, :Fs4, :E4, :Cs5, :B4, :Fs4, :D5)

live_loop :piano, sync: :met do
  
  6.times do
    use_synth :piano
    play notes.choose, amp: 0.5, release: 0.1
    sleep 0.25
  end
  
  1.times do
    play notes.tick , amp: 0.7, release: 3, sustain: 2
    sleep 4
  end
end
```

Used an array of notes for the piano, i.e `notes = (ring :E4, :Fs4, :B4, :Cs5, :D5, :Fs4, :E4, :Cs5, :B4, :Fs4, :D5)`. 

Then, the computer chooses a note 6 times in the first loop: 

``` ruby
  6.times do
    use_synth :piano
    play notes.choose, amp: 0.5, release: 0.1
    sleep 0.25
  end
```

And ticks through the array once every loop for the 7th note: 

``` ruby
  1.times do
    play notes.tick , amp: 0.7, release: 3, sustain: 2
    sleep 4
  end
```

21:15, 2024-05-21

***
### making a hand-synthesiser #p5
Using my previous study on hand landmarks, I made a synthesiser that operates via the hand. 

![[Screen Recording 2024-05-15 at 12.54.48 PM.mov]]

First, the program calculates the distance between each finger on a single hand and returns this distances. 

``` js
function distCalc() {
  var dIndex = dist(thumbTip[0], thumbTip[1], indexTip[0], indexTip[1]);
  var dMid = dist(thumbTip[0], thumbTip[1], middleTip[0], middleTip[1]);
  var dRing = dist(thumbTip[0], thumbTip[1], ringTip[0], ringTip[1]);
  var dPinky = dist(thumbTip[0], thumbTip[1], pinkyTip[0], pinkyTip[1]);

  textAlign (LEFT); 
  textSize(10);
  fill(0);
  noStroke();
  text("thumb-index: " + int(dIndex), 50, 30 + 15);
  text("thumb-middle: " + int(dMid), 50, 30 + 30);
  text("thumb-ring: " + int(dRing), 50, 30 + 45);
  text("thumb-pinky: " + int(dPinky), 50, 30 + 60);

  textAlign(RIGHT); 

  text ("frequency playing: "+ freqPlaying, width-50, 30+15); 

  perform(
    dIndex,
    dMid,
    dRing,
    dPinky,
    thumbTip[0],
    indexTip[1],
    middleTip[1],
    ringTip[1],
    pinkyTip[1]
  );
}
```

Then, a function called 'perform' maps distances to frequencies based on the 'note' assigned to each finger (index is A, middle is B ... and so on). Furthermore, horizontal position of the thumb determines the amplitude whereas vertical position of the fingers determine the pitch (high to low). 

``` js
function perform(
  dIndex,
  dMid,
  dRing,
  dPinky,
  thumbTipX,
  indexTipY,
  middleTipY,
  ringTipY,
  pinkyTipY
) {
  //Changing amplitude based on horizontal position of thumb on screen.
  amp = constrain(map(thumbTipX, width, 0, 0, 1), 0, 1);

  //Mapping frequencies to position of finger on screen. 
  //Used music references from Tom Cortina's Class: 15-104 Introduction to Computing for Creative Practice (24, More Sound). 
  indexFreq = map(indexTipY, height, 0, 27.5, 880); //A0-A5
  middleFrequency = map(middleTipY, height, 0, 30.868, 987.77); //B0-B5
  ringFrequency = map(ringTipY, height, 0, 32.703, 1046.5); //C1-C6
  pinkyFrequency = map(pinkyTipY, height, 0, 43.654, 1318.5); //E1-E6

  //Consider boilerplate for playing. True means amp is set based on the mapping and oscillator starts, else oscillator amp is 0.
  if (playing) {
    osc.amp(amp, 0.1);
    osc.start();
    playing=false;
  } else {
    osc.amp(0, 0.1);
  }

  //Main playing mapping – each bucket takes a distance threshold and plays a certain frequency.
  if ((dIndex <= 80) & (dIndex != 0)) {
    //for index
    osc.freq(indexFreq, 0.1);
    playing = true;
    freqPlaying = indexFreq; 
  } else if ((dMid <= 80) & (dMid != 0)) {
    //for middle
    osc.freq(middleFrequency, 0.1);
    playing = true;
    freqPlaying = middleFrequency; 
  } else if ((dRing <= 80) & (dRing != 0)) {
    //for ring
    osc.freq(ringFrequency, 0.1);
    playing = true;
    freqPlaying = ringFrequency;
  } else if ((dPinky <= 80) & (dRing != 0)) {
    //for pinky
    osc.freq(pinkyFrequency, 0.1);
    playing = true;
    freqPlaying = pinkyFrequency;
  }else if (dPinky <= 80 & dMid<=80 & dRing<=80 & dIndex<=80){ //Fingers are clumped or off the screen, so play nothing.
    playing = false;
  } else {
    freqPlaying = 0; 
    playing = false;
  }
}
```

Try to make a song from this? Program available here: https://arjunmakesthings.github.io/hand-synthesiser/index.html

13:06, 2024-05-15

***
### accessing specific landmarks #p5 
After filling predictions array with results, one can access specific parts of the landmarks according to this diagram: 

![[HandLandmarks_MediaPipe.png]]

``` js
//Using specific landmarks

  if (predictions.length > 0) {
    let hand = predictions[0].landmarks; // Extracting landmarks from the first prediction
  
    // Accessing specific landmark points
    let thumbTip = hand[4]; // Thumb tip
    let indexTip = hand[8]; // Index finger tip
    let middleTip = hand[12]; // Middle finger tip
    let ringTip = hand[16]; // Ring finger tip
    let pinkyTip = hand[20]; // Pinky finger tip
    
    }
```

13:50, 2024-05-05
***
### rotational studies #p5 
Messed around with earlier rotational studies. Re-used the idea of a particle moving in a circular motion from the previous program. 

``` js
//Base 
  for (let x = margin; x <= width - margin; x += s) {
    for (let y = margin; y <= height - margin; y += s) {
      let x1 = cos(x + inc) * diam;
      let y1 = sin(y + inc) * diam;

      push();
      translate(x1, y1);
      square(x, y, s, s / 8); //used rounding of corners for squares
      pop();
    }
  }

inc += 0.02;
```

![[Screen Recording 2024-04-18 at 2.07.20 PM.mov]]

If I let the program draw itself out without replacing the background, it looks like this: 

![[Screenshot 2024-04-18 at 2.08.45 PM.png]]

Parameter changes (such as diameter incrementing / spacing between individual squares) result in these: 

![[some.mov]]

14:14, 2024-04-18

***
### we go around in circles #p5 
Still working on typographic treatment using interesting waves. Thought about each particle rotating in a circle by using cos and sin waves. 

``` js
  let x = cos(angle) * circleRadius;
  let y = sin(angle) * circleRadius;
  
  // while
  angle +=0.02
```

![[1 1.mov]]

Also thought of a neat way to assign colours. Once particles are assigned an x & y coordinate: 

``` js
//declare array of colours
let col = ['#941b0c', '#bc3908', '#f6aa1c'];

// run through x / y array and assign random value from colour array.
  for (let i = 0; i<xPos.length; i++){
    n.push(random(col)); 
  }

// in draw
fill (n[i]);
```

For size, I also used noise for some variability. Main draw code: 

``` js
function draw() {
  background("#130108");

  for (let i = 0; i < xPos.length; i += 1) {
    let x = cos(i + mult) * diam;
    let y = sin(i + mult) * diam;

    fill(n[i]);
    ellipse(xPos[i] + x, yPos[i] + y, (noise(x) * 30) / 2.2); // I think the division is redundant but somehow it reduced speed of the particles (?)
  }

  mult += inc;
}
```

16:54, 2024-04-15

***
### boilerplate for hand-tracking #p5 #ml5
Simple boilerplate for single hand tracking. Going to use it for the body synthesizer. Used a bit of ChatGPT to understand what's happening. 

![[Screen Recording 2024-04-14 at 12.33.30 PM.mov]]

``` js
//Single Hand Tracker

let video;
let handpose;
let predictions = [];

function setup() {
  createCanvas(640, 480);
  video = createCapture(VIDEO);
  video.hide();
  handpose = ml5.handpose(video, modelReady);
  handpose.on('predict', gotPredictions);
}

//To tell whether model has loaded or not
function modelReady() {
  text ("Model loaded", 50, 50); 
}

function gotPredictions(results) {
  predictions = results;
}

function draw() {
  background(255);
  
  // Flip the video horizontally to match hand to video
  translate(width, 0);
  scale(-1, 1);
  image(video, 0, 0, width, height);
  drawKeypoints();
}

function drawKeypoints() {
  for (let i = 0; i < predictions.length; i++) {
    let prediction = predictions[i];
    for (let j = 0; j < prediction.landmarks.length; j++) {
      let point = prediction.landmarks[j];
      fill(255, 0, 0);
      noStroke();
      ellipse(point[0], point[1], 10, 10);
    }
  }
}
```

12:36, 2024-04-14
***
### light shining on waterbody in the night #p5
Was inspired by lights glimmering on a waterbody, seen during the night on my last trip to Ahmedabad (near the Riverfront). 

Made this while listening to Perfect by Ed Sheeran. 

![[2 1.mov]]

``` js
  for (let i = 0; i < xPos.length; i += 2) {
    let wave = sin(i + waveOffset) * waveHeight;

    line(xPos[i] + wave, yPos[i], xPos[i], yPos[i]);
  }
  // Update wave offset for animation
  waveOffset += waveSpeed;
```

I like how it came out. You can also play around with the parameters, manipulating the legibility. 

![[1.mov]]

17:32, 2024-04-12
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


