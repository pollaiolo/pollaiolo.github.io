---
layout: post
title:  "A matter of physics: buoncing balls + leap + p5.js"
subtitle: "F equals M times A"
date:   2017-09-05 23:34:01
comments: true
categories: [physics]
published: true
---

Explaining natural phenomena with math is called *physics* and has been one of the human goal since we exist. We are sorrounded by physics, when we stand up we fight against the gravitational attraction that wants us to sit.\\
However, there is a place where no physics law exists and nothing really happens. I'm talking about the virtual space we usually work with: software. Even if I'm writing this, there's no ink who wets the paper but you're still able to read this post. Softwares create a virtual place where we can do everything we do in reality but without struggling with physics laws.

What I'd like to show here is an introduction to how we can model physics laws in a virtual place and interact with it. The virtual space will be an html canvas, the physics law will be the [Newton's second law](https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion) and our interaction will be through a [leap motion](https://www.leapmotion.com/) device.
## p5*js
In this project I'm using [p5.js](https://p5js.org/) to help me with physics and rendering. This library is quite popular and powerfull; it doesn't do anything more than calling a function once `setup()` and another one forever `draw()`. 
Let's create a new html page importing the libraries we'll use in this project:
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
