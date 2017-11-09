---
layout: post
title:  "It's a matter of physics: buoncing balls with leap and p5.js"
subtitle: "F equals M times A"
date:   2017-09-05 23:34:01
comments: true
categories: [physics]
published: true
---

Explaining natural phenomena with math is called *physics* and has been one of the human goal since we exist. We are sorrounded by physics, when we stand up we fight against the gravitational attraction that wants us to sit.\\
However, there is a place where no physics law exists and nothing really happens. I'm talking about the virtual space we usually work with: our personal computer. Even if I'm writing this, there's no ink who wets the paper but you're still able to read this post. Programs create a virtual place where we can do everything we do in reality but without struggling with physics laws.

What I'd like to show here is an introduction on how we can model physics laws in a virtual place and interact with it. The virtual space will be an `HTML` canvas, the physics law will be the [Newton's second law][https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion] and our interaction will be through [leap motion][https://www.leapmotion.com/] device.\\
In this project I'm using [p5.js][https://p5js.org/] to help me with physics and rendering. This library is quite popular and powerfull, it doesn't do anything more than calling a function forever, this one:
``` javascript
function draw() {
	background(127);
	frame = controller.frame();
	if (frame.fingers.length > 2) {
		for (var i = balls.length - 1; i > 0; i--) {
			balls[i].applyForce(forceRHand);
		}
	}
	if (frame.hands.length > 1) {
		for (var i = balls.length - 1; i > 0; i--) {
			balls[i].applyForce(forceLHand);
		}
	}
	for(var i = balls.length - 1; i > 0; i--) {
		var gravity = createVector(0, balls[i].mass);
			balls[i].applyForce(gravity);
			balls[i].update();
			balls[i].display();
			balls[i].bounce();
	}
}
```

