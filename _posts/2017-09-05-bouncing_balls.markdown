---
layout: post
title:  "A matter of physics: buoncing balls"
subtitle: "F = M * A"
date:   2017-09-05 23:34:01
comments: true
categories: [physics]
published: true
---

Explaining natural phenomena with math is called *physics* and has been one of the human goal since we exist. We are sorrounded by physics, when we stand up we fight against the gravitational attraction that wants us to sit.\\
However, there is a place where no physics law exists and nothing really happens. I'm talking about the virtual space we usually work with: software. Even if I'm writing this, there's no ink who wets the paper; softwares create a virtual place where we can do everything we do in reality but without struggling with physics laws.

What I'd like to show here is an introduction to how we can model physics laws in a virtual place and interact with it. The virtual space will be an `html` canvas, the physics law will be the [Newton's second law](https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion) and our interaction will be through a [leap motion](https://www.leapmotion.com/) device.

## p5*js
In this project I'm using [p5*js](https://p5js.org/) to help me with physics and rendering. This library is quite popular and powerfull; it doesn't do anything more than calling a function once `setup()` and another one forever `draw()`. 
Let's start creating a new html page importing the libraries we'll use in this project:
{%highlight html%}
<!DOCTYPE html>
<html>
   <head>
      <script src="https://js.leapmotion.com/leap-0.6.4.js"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.11/p5.js"></script>
      <script src="ball.js"></script>
      <script src="sketch.js"></script>
      <title>Sketch</title>
    </head>
</html>
{%endhighlight%}
``sketch.js`` file will contain p5*js functions, just setup a new canvas in the page and draw a gray background every iteration:
{%highlight javascript%}
function setup() {
   createCanvas(windowWidth - 20, windowHeight - 20);
}
function draw() {
   background(160);
}
{%endhighlight%}

## Leap Motion
Leap is a device to track hands. It has two cameras and an infrared sensor to track up to 10 moving fingers (two hands, in other words). It offers usefull **API** to easily detect, in each captured frame, the position of hands, fingers and arms. Let's wire this into our program:      
{%highlight javascript%}
function setup() {
   createCanvas(windowWidth - 20, windowHeight - 20);
   controller = new Leap.Controller();
   controller.connect();
}

function draw() {
   background(127);
   frame = controller.frame();
   if (frame.hands.length > 1) {
      background(1);
   }
}
{%endhighlight%}
Now everytime two hands are detected the background of the canvas is set to black.

## Physics
If you've ever studied physics (I suppose you did) you'd know about forces. A force is a vector applied to an object which can cause a change in its *velocity*. Here I'm referring to the physics concept of velocity:\\
*Velocity is a **physical vector** quantity; both magnitude and direction are needed to define it.*

The force I'm using in this project is an *acceleration* controlled by the hand recognized with leap controller; whenever two hands are recognized a double acceleration is applied to the balls. The hands apply a vertical acceleration to the balls contrasting the gravitational attraction. The vectors associated with those forces are: `forceRHand = createVector(0, -150)` and `forceLHand = createVector(0, -150)`. \\
While the gravitational attraction is `gravity = createVector(0, balls[i].mass)`.\\
As you can see the vector's magnitude is proportional to the mass of the ball (this is just a semplification and doesn't correspond exactly to earth gravity).  

**p5*js** has nice functions to help working with vectors including math operations. In this project I'm using balls as objects and each one will be represented by three vectors (position, velocity and acceleration) and a scalar (mass):
{%highlight javascript%}
function Ball(x, y, m) {

   this.mass = m;
   this.position = createVector(x, y);
   this.velocity = createVector(0, 0);
   this.acceleration = createVector(0, 0);

   this.display = function() {
      stroke(2);
      ellipse(this.position.x, this.position.y, this.mass, this.mass);
   }

   this.applyForce = function(acceleration) {
      var acc = p5.Vector.div(acceleration, this.mass);
      this.acceleration.add(acc);
   }

  this.update = function() {
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
      this.acceleration.mult(0);
   }

   this.bounce = function() {
      // reminder omitted here
   }
{%endhighlight%}
Every time the `draw()` function is called from **p5*js** it will perform those actions on the ball:
1. `applyForce` to apply gravitational acceleration and possible other forces.
   Applying a force to the ball means applying the Newton's Second Law $$ F=M*A $$ to find out how the object is changing it's acceleration. In this example the formula would be: $$ A=F/M $$ where $$ F $$ is the current force (acceleration) applied to the ball. The obtained value is then added to the actual acceleration.
2. `update` to update the vectors describing the ball.
   Vectorial sums are performed to update every ball component; acceleration is added to the velocity and velocity is added to position. The acceleration vector is then set to 0 since this force is not continuous in time.
3. `diplay` to show the ball in the canvas.
4. `bounce` to check if the ball is touching the edges of the canvas.
   There's another force considered in this function: `friction`. This vector opposes to the ball when rolling and pushes it, proportionally to its mass, in the opposite direction. Check the sources for details.

The `sketch.js` function will be then composed as follow:
{%highlight javascript%}
var balls = [];
var controller;
var frame;

function setup() {
   createCanvas(windowWidth - 20, windowHeight - 20);
   forceHand = createVector(0, -150);
   controller = new Leap.Controller();
   controller.connect();
   for (var i = 10; i > 0; i--) {
      balls[i] = new Ball(random(10, width), height - 200, random(20, 40));
   }
}
 
function draw() {
   background(160);
   frame = controller.frame();
   for(var i = balls.length - 1; i > 0; i--) {
      if (frame.hands.length == 1) {
         balls[i].applyForce(forceHand);
      } else if(frame.hands.length == 2) {
         balls[i].applyForce(forceHand);
         balls[i].applyForce(forceHand);
      }
      var gravity = createVector(0, balls[i].mass);
      balls[i].applyForce(gravity);
      balls[i].update();
      balls[i].display();
      balls[i].bounce();
   }
}
{%endhighlight%}

Since the **leap** controller is not widely used keyboard controls are added to sources. You can play it around using your arrow keys.  