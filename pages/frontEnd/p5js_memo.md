---
# layout: note_tutorial
title: p5js
catalog: true
tags: 
  - javascript
  - function expression
permalink: p5_js.html
folder: frontEnd
summary: 
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## `setup()` and `draw()` function

The setup function happens only once.

```
function setup() {

}
```

And the draw function just loops.

```
function draw() {

}
```

In most cases, we place background definition within `draw`. What is we nest it under `setup`?

Remember? `setup` loads only once. So the background will not refresh when drawing behaviors leave their marks. That is to say, we are able to take advantage of it to make a painting panel, like this:

```
function setup() {
  createCanvas(600, 400);  background(120, 100, 200);
}

function draw() {


  // ellipse
  noStroke();
  fill(250, 200, 200,50);
  ellipse(mouseX, mouseY, 30, 30);
```

You may even enable it to clear the window upon a mouse click.

```
function setup() {
  createCanvas(600, 400);  background(120, 100, 200);
}

function draw() {


  // ellipse
  noStroke();
  fill(250, 200, 200,50);
  ellipse(mouseX, mouseY, 30, 30);

}

function mousePressed() {
  background(120, 100, 200);
}
```

## Declaring a variable

Wield JSON (JavaScript Object Notation) to organize variables related to the same element.

```
var myCircle1 = {
  x: 0,
  y: 100,
  diameter: 50
};

var myCircle2 = {
  x: 400,
  y: 400,
  diameter: 400,
};
```

To implement variables, use dot notation:

```
myCircle1.x++;
```

```
ellipse(myCircle1.x, myCircle1.y, myCircle1.diameter, myCircle1.diameter);
```

### Homework: Draw two animated circles

```
// JavaScript Object Notation (JSON)
var myCircle1 = {
  x: 0,
  y: 100,
  diameter: 50
};

var myCircle2 = {
  x: 800,
  y: 400,
  diameter: 700,
};

function setup() {
  createCanvas(800, 500);
}

function draw() {
  background(120, 100, 200);
  myCircle1.x++;
  myCircle1.y++;
  myCircle1.diameter++;
  fill(200, 100, 80);
  noStroke();
  // dot syntax: 
  ellipse(myCircle1.x, myCircle1.y, myCircle1.diameter, myCircle1.diameter);
  myCircle2.x--;
  myCircle2.y--;
  myCircle2.diameter--;
  fill(100, 200, 100);
  ellipse(myCircle2.x, myCircle2.y, myCircle2.diameter, myCircle2.diameter);
}
```

## `map()` function

> Description: Re-maps a number from one range to another

**Task**: Get the background light up as you move your mouse towards the right side of the canvas, and black out again when you returns to the left side.

### Analysis

-   The *background color* changes with the *horizontal position of your mouse*, `mouseX`.
-   The background color scheme ranges from 0 (total blackness) to 255 (absolute white), and the mouseX from 0 (leftmost) to 255 (rightmost)

### Arguments in `map()` function

You should pass in 5 parameters in a `map()` function. Let's also take the target variable into account, so we've got 6 items to specify.

```
targetVariable = map(sourceVariable, sourceStart, sourceEnd, targetStart, targetEnd);
```

So, in this case, it should go like this:

```
var col = 0;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(col);
  col = map(mouseX, 0, 600, 0, 255);
  fill(200,100,30);
  noStroke();
  ellipse(mouseX, mouseY, 40,40);
}
```

## random()

Picks up a random floating number within the given range.

```
random([min], [max])
```

or

```
random(choices)
```

`choices`: the array to choose from

### A nice example

```
var myPoint = {
  x: 100,
  y: 50
};

var col = {
  r: 255,
  g: 0,
  b: 0
};

function setup() {
  createCanvas(600, 400);
  background(0);
}

function draw() {
  col.r = random(100, 255);
  col.g = 0;
  col.b = random(100, 190);
  myPoint.x = random(0, width);
  myPoint.y = random(0, height);
  fill(col.r, col.g, col.b, 100);
  noStroke();
  ellipse(myPoint.x, myPoint.y, 24, 24);
}
```

## Condition

### Exercise: Bouncing ball

```
var x = 54;
var speedX = 3;
var y = 54;
var speedY = 3;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(0);

  stroke(255);
  strokeWeight(4);
  noFill();

  ellipse(x, y, 100, 100);


  if (x > width - 54) {
    speedX = -3
  }
  if (x < 54) {
    speedX = 3;
  }
  if (y > height - 54) {
    speedY = -3
  }
  if (y < 54) {
    speedY = 3;
  }
  x = x + speedX;
  y = y + speedY;

}
```
This is verbose. Let's make a polish.

```
var x = 54;
var speedX = 3;
var y = 54;
var speedY = 3;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(0);

  noStroke();
  fill(x/2, 255, y/2);

  ellipse(x, y, 100, 100);


  if (x > width - 50 || x < 50) {
    speedX = speedX * -1;
  }
  if (y > height - 50 || y < 50) {
    speedY = speedY * -1;
  }
  x = x + speedX;
  y = y + speedY;

}
```

### `if` statement

You can have as many `else if` as you want in between an `if` statement.

Within an `if` statement, the order really matters. Once the program detects a true expression, it omits its follow-up peers and peels away from the entire `if` block.

## Distinction between `mouseIsPressed` and `function mousePressed()`

`mouseIsPressed` is a boolean. It gets use when the mouse is being clicked, a state.

`function mousePressed()` is to execute certain behaviors upon the click of the mouse.

  // rollover is a JavaScript technique used by Web developers to produce an effect in which the appearance of a graphical image changes when the user rolls the mouse pointer over it. Rollover also refers to a button on a Web page that allows interactivity between the user and the Web page.

```
var on = false;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  if (on) {
    background(0, 255, 0);
  } else {
    background(0);
  }

  stroke(255);
  strokeWeight(4);
  noFill();
  rectMode(CENTER);
  rect(300, 200, 100, 100);
}

function mousePressed() {
  if (mouseX > 250 && mouseX < 350 && mouseY > 150 && mouseY < 250) {
    if (on) {
      on = false;
    } else {
      on = true;
    }
  }
}
```

### not operation `!`

Q: Does `if(!on)` make sense?
A: Absolutely YES!

```
on = !on
```
Set the value of this variable to ***not itself***.
So if its value is false, not false is true. If its value is true, not true is false.

`speed = speed * -1` reverts toggles the number between positive and negative, while `on = !on` toggles a boolean back and forth.

So we may simply condense the code block that purports to toggle a boolean variable down to one line.

Transition the old super wordy code block:

```
if (on) {
      on = false;
    } else {
      on = true;
    }
```

to:

```
on = !on;
```

## `while` loops

-   `while` loops start with initialization of a variable. Don't put the variable at the beginning of your program as you did so in an `if` statement previously.
-   You should test an exit condition to make sure the looping stops at a proper time.
-   Append an incrementation operation.

Here's an example: 

```
function setup() {
  createCanvas(600, 400);

}

function draw() {
  background(0);

  strokeWeight(4);
  stroke(255);
  var x = 0;
  while (x <= width) {
    ellipse(x, 200, 25, 25);
    x = x + 50;
  }
}
```

It has the above-mentioned three elements, right? Let's convert it to a `for` expression. You are good to go.

```
for (var x = 0; x <= width; x = x + 50) {
  ellipse(x, 200, 25, 25);
}
```

It also works.

### Shorthand expression

`x = x + 50` can be written shorthand as `x += 50`, and `x = x + 1` `x++`.

### Exercise

Get the ellipses repeat every 50 pixels, with ascending or descending opacity.

var colAlpha = 0;
var colAlpha2 = 80;

function setup() {
  createCanvas(600, 400);

}

function draw() {
  background(0);


  strokeWeight(4);
  stroke(255);
  var x = 0;
  while (x <= width) {
    colAlpha = map(x, 0, 600, 30, 100);
    fill(0, 200, 255, colAlpha);
    ellipse(x, 100, 25, 25);
    x += 50;
  }

  for (var x = 0; x <= width; x = x + 50) {
    colAlpha2 = map(x, 0, 600, 100, 30);
    fill(255, 0, 100, colAlpha2);
    ellipse(x, 200, 25, 25);
  }

}

### Canvas loading time

How long does it take the program to draw the numerous shapes in the previous example?

Why all of them just appear the instant the page loads? Is it that the drawing behaviors just happens so fast that they elude us?

Not actually. The canvas is not updated until the end of `draw()` is reached. That is because the purpose of a `draw()`function is to draw a whole bunch of things , rather than to animate something. If you want to do animation, you've got to change slightly.

The `draw()` function is for the purpose of refreshing that "flip book" metaphor. And as for the `for` block, there's no flip book there. It intends to perform a repeating task on a single page in the flip book for animation.

### Nesting loops

```
function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(0);
  strokeWeight(4);
  stroke(255);
  
  for (var x = 0; x <= width; x += 50) {
  for (var y = 0; y <= height; y += 50) {
  fill(random(255), 0, random(255));
    ellipse(x, y, 25, 25);
  }
  }
}
```

<p><iframe width="600" height="400" frameborder="0"  src="https://editor.p5js.org/uufishtxl/embed/Q_04vWP1H"></iframe></p>

## Functions

### Calling vs defining

Both `ellipse()` and `function setup() {}` are P5 functions. They live within P5. They belong to the P5's library of functions. Still, there's something strange going. When you use `ellipse()`, we simpled ***call*** the function. As for `function setup() {}`, we are ***defining*** the function. And P5 extends a hand to us because he knows when to execute it.

That said, can we define our own functions? Of couse. We define and call our own functions for the purpose of:

-   Modularity
-   Reusability：this is where arguments/ parameters come along.

### Demo

Let's organize the bouncing ball program into modularized functions and call such functions to do the desired animation.

Steps: 

1.   Segment the behaviors into three different modulars:
     -   `function move () {}`: controls the movement
     -   `function bounce() {}`: controls direction switch
     -   `function display() {}`: specifies the details of the shape
2.  Call the customized three functions.

By modularizing functions, you may test on different function modules independently.

```
var ball = {
  x: 300,
  y: 200,
  xSpeed:  4,
  ySpeed: -3
}


function setup() {
  createCanvas(600, 400);
}


function draw() {
  background(0);
  move();
  bounce();
  display();
}


function move() {
  ball.x = ball.x + ball.xSpeed;
  ball.y = ball.y + ball.ySpeed;
}


function bounce () {
  if (ball.x > width - 17 || ball.x < 17) {
    ball.xSpeed = ball.xSpeed * -1;
  }
  if (ball.y > height - 17 || ball.y < 17) {
    ball.ySpeed = ball.ySpeed * -1
  }
}


function display() {
  stroke(255);
  strokeWeight(4);
  fill(200, 100, 100);
  ellipse(ball.x, ball.y, 25, 25)
}
```

## Define a function with parameters

Arguments in a function come from where you call the function. You don't define it with a `var x = 0` expression. That is to say, you simply name the variables in in between the parenthesis and quote them in the curly brace of the function. When you call a function, of course you will pass in parameters. As long as the parameters you passed in match the pre-configured parameter schemes when you define that specific function, everything works without complications.

```
function setup() {
  createCanvas(600, 600);
}

function draw() {

  lollipop(200, 300, 100);
  lollipop(100, 150, 80);


}

function lollipop(x, y, diameter) {
  fill(0, 200, 255);
  noStroke();
  rect(x - 10, diameter / 2 + y - 5, 20, 150);

  fill(255, 0, 200);
  noStroke();
  ellipse(x, y, diameter, diameter);


}
```

## Object literals

> In particular, if what I want to do is to program graphics, simulations, animations, things moving around the screen, one way to do that is to think about this circle moving around as an object. The bubble, it has data, that is x and y as its coordinate positions,  as well as ***a behavior***.

### Encapsulation

> So now we come to the `encapsulation` process. We like to encapsulate everything that is to be a certain thing inside of an object. What properties does a bubble have? What things do they do throughout their life?

Class is a template, or a blueprint.

```
class Bubble {
  ...
}
```

A function within a class is to ***construct*** an object.

```javascript
let bubble1;
let bubble2;

function setup() {
  createCanvas(800, 600);
  bubble1 = new Bubble(300, 300, 30);
  bubble2 = new Bubble(400, 350, 10);
}

function draw() {
  background(0);
  bubble1.move();
  bubble1.show();
  bubble2.move();
  bubble2.show();
}

class Bubble {
  constructor(x, y, r) {
    this.x = x;
    this.y = y;
    this.r = r;
  }
  
  move() {
    this.x = this.x + random(-10, 10);
    this.y = this.y + random(-5, 5);
  }
  
  show() {
    stroke(255);
    strokeWeight(4);
    noFill();
    ellipse(this.x, this.y, this.r*2, this.r*2);
  }
}
```

Right now, `this` is a reference to the current object instance. We can't just quote the variable name here. We have to specify the exact value for a particular object instant by using this. expression.

```
var nums = [100, 25, 46, 72]
var index = 0

function setup() {
  createCanvas(500, 400);
}

function draw() {
  background(0);

  for (var i = 0; i < 4; i++) {
    stroke(255);
    fill(255);
    ellipse(100 * i + 100, 200, nums[i], nums[i]);
  }

}
```

> What is interesting about JavaScript is if the array is empty and you just assgin something to the first spot, and then assign something to the second spo, then just assigning the third spot, JavaScript will just like I'm going go figure out what you're doing. I'l just make the array the right size for what you're putting it.

Process of Polish

```JavaScript
var bubbles = [];


function setup() {
  createCanvas(600, 400);
  for (var i = 0; i < 504; i++) {
    bubbles[i] = {
      x: random(0, width),
      y: random(0, height),
      display: function() {
        stroke(0);
        fill(255);
        ellipse(this.x, this.y, 24, 24);
      },
      move: function() {
        this.x = this.x + random(-5, 5);
        this.y = this.y + random(-5, 5);
      }
    }
  }
  
  // print(bubbles);
}

function draw() {
  background(0);
  for (var i = 0; i < bubbles.length; i++) {
    bubbles[i].move();
    bubbles[i].display();
  }
}
```

Make some refinement. Get rid of the variable making approach in favor of a constructor function.

```
var bubbles = [];


function setup() {
  createCanvas(600, 400);
  for (var i = 0; i < 504; i++) {
    bubbles[i] = new Bubble();
  }

  // print(bubbles);
}

function draw() {
  background(0);
  for (var i = 0; i < bubbles.length; i++) {
    bubbles[i].move();
    bubbles[i].display();
  }
}


function Bubble() {
  //   The new object the constructor has made attach the property x to this bubble object
  this.x = random(0, width);
  this.y = random(0, height);

  this.display = function() {
    stroke(0);
    fill(255);
    ellipse(this.x, this.y, 24, 24);
  }

  this.move = function() {
    this.x = this.x + random(-1, 1);
    this.y = this.y + random(-1, 1);
  }

}

```

If you provide argument parameter to your constructor function, 


## Scenario: Overlapping or not?

See if two bubbles overlap with each other or stay away from each other. Toggle the background back and forth to announce the transition.

```JavaScript
let bubble1;
let bubble2;

function setup() {
  createCanvas(600, 400);
  bubble1 = new Bubble(300, 100);
  bubble2 = new Bubble(250, 100, 100);
}

function draw() {
  background(0);

  let d = dist(bubble1.x, bubble1.y, bubble2.x, bubble2.y);
  
  if (d < bubble1.r / 2 + bubble2.r / 2) {
    background(220, 0, 10);
  }
  bubble1.move();
  bubble1.show();
  bubble2.move();
  bubble2.show();
}

class Bubble {
  constructor(x, y, r = 50) {
    this.x = x;
    this.y = y;
    this.r = r;
  }

  move() {
    this.x = this.x + random(-2, 2);
    this.y = this.y + random(-2, 2);
  }

  show() {
    stroke(255);
    strokeWeight(4);
    noFill();
    ellipse(this.x, this.y, this.r, this.r);
  }

}
```

The above program is able to check out the distance between two bubbles. What if I would like to get the bubble itself to communicate with others to check out the distances? Let's make some upgrade by also encapasulating a function like `if(b1.intersects(b2)){}` into the class constructor.


So, the function we'd like to build into the class is something like `if(b1, intersect(b2)) {}`. b2 is an actual parameter, so let's name the parameter itself `other`. The so called `other` is a bubble, an actual object built off the template `Bubble`. The coordinate of its central position goes as `other.x` and `other.y`. So it is clear as day that to find the distance, we can just go this way: `dist(this.x, this.y, other.x, other.y)`.


```JavaScript
let bubble1;
let bubble2;

function setup() {
  createCanvas(600, 400);
  bubble1 = new Bubble(300, 100);
  bubble2 = new Bubble(250, 100, 100);
}

function draw() {
  background(0);

  if (bubble1.intersect(bubble2)) {
    background(220, 0, 10);
  }
  bubble1.move();
  bubble1.show();
  bubble2.move();
  bubble2.show();
}

class Bubble {
  constructor(x, y, r = 50) {
    this.x = x;
    this.y = y;
    this.r = r;
  }

  move() {
    this.x = this.x + random(-2, 2);
    this.y = this.y + random(-2, 2);
  }

  show() {
    stroke(255);
    strokeWeight(4);
    noFill();
    ellipse(this.x, this.y, this.r, this.r);
  }

  intersect(other) {
    let d = dist(this.x, this.y, other.x, other.y);
    if (d < this.r / 2 + other.r / 2) {
      return true;
    } else {
      return false;
    }
  }

}
```

Now, let's shift our focus onto the if statement. The whole block can be further simplified. Given that the `d < this.r / 2 + other.r / 2)` is a statement, we don't have to expand to the verbose `return true` and `return false` parts. Just code it this way.

```JavaScript
let d = dist(this.x, this.y, other.x, other.y)
return (d < this.r / 2 + other.r / 2);
```


```JavaScript
let bubbles = [];
// let unicorn;

function setup() {
  createCanvas(600, 400);

  for (let i = 0; i < 10; i++) {
    let x = random(width);
    let y = random(height);
    let r = random(10, 50);
    bubbles[i] = new Bubble(x, y, r);
  }

  // unicorn = new Bubble(400, 200, 10);
}

function draw() {
  background(0);
  //   for (let i = 0; i < bubbles.length; i++) {
  //     bubbles[i].show();
  //     bubbles[i].move();
  //   }


  for (let b of bubbles) {
    b.show();
    b.move();
    let overlapping = false;
    for (let other of bubbles) {
      if (b != other && b.intersect(other)) {
        overlapping = true;
      // } else {
      //   b.changeColor(0);
      // 
      }
    }
    
    if (overlapping) {
      b.changeColor(255);
    } else {
      b.changeColor(0);
    }
    
  }
  // unicorn.x = mouseX;
  // unicorn.y = mouseY;
  // unicorn.move();
  // unicorn.show();
}

class Bubble {
  constructor(x, y, r = 50) {
    this.x = x;
    this.y = y;
    this.r = r;
    this.brightness = 0;
  }

  move() {
    this.x = this.x + random(-1, 1);
    this.y = this.y + random(-1, 1);
  }

  show() {
    stroke(255);
    strokeWeight(4);
    fill(this.brightness, this.brightness, this.brightness, 100);
    ellipse(this.x, this.y, this.r * 2, this.r * 2);
  }

  intersect(other) {
    let d = dist(this.x, this.y, other.x, other.y);
    return (d < this.r + other.r);
  }

  changeColor(bright) {
    this.brightness = bright;
  }
}
```