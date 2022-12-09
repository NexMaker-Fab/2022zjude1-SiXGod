# processing & P5.js

### 1  Try to find something similar to processing?

Processing is an open source software platform for creating animations and interactive graphics. It has a simple and easy-to-use programming language that allows users to create and publish interactive graphic works. If you are looking for something similar to Processing, there are several software platforms to consider:

- p5.js：This is a JavaScript library for creating interactive graphics. Its syntax is very similar to Processing and allows users to easily create interactive graphics in their browser.
- OpenFrameworks：This is a C++ library for creating art and interactive works. It provides developers with a rich library that supports a variety of input and output devices, including touch screens, cameras, and microphones.
- Cinder：This is a C++ library for creating 2D and 3D graphic works. It provides developers with a wealth of tools that allow them to create complex graphics and animations.
  
In addition to the tools described above, there are many other processing-like software platforms, including Rune.js, Quil, and Khan Academy.

### 2  Try ps5.js mode in processing

Here is a piece of visual code for the free fall of a ball written in P5.js:

```jsx
let x = 100; // The abscissa of the ball
let y = 0; // The ordinate of the ball
let v = 0; // The velocity of the ball
let g = 0.1; // acceleration of gravity

function setup() {
  createCanvas(400, 400);
  background(0);
}

function draw() {
  fill(255);
  ellipse(x, y, 50, 50); // Draw the ball
  v += g; // update velocity
  y += v; // update position
  if (y > height) { // If the ball lands
    y = height; // Set the ordinate of the ball to the ground height
    v = -v; // Bounce of the ball
  }
}
```

This code can draw a small ball on a canvas and simulate its free-fall motion.

Instructions for online compilation are as follows:

1. Open the official website of P5.js in a web browser: **[https://p5js.org/](https://p5js.org/%E3%80%82)**
2. Click the "Get Started" button at the top of the page to enter the P5.js tutorial page.
3. Click the "Start Coding" button in the tutorial page to open the P5.js editor.
4. Enter the code mentioned above in the editor, then click the "Run" button to run the code.
5. Viewing the results in a browser, you can see a small ball on the canvas in free fall motion.

<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/p5js.png?raw=true" width = "1000" />
</div>
<br></br>

First, this code defines several variables:

```jsx
let x = 100; // The abscissa of the ball
let y = 0; // The ordinate of the ball
let v = 0; // The velocity of the ball
let g = 0.1; // acceleration of gravity
```

Among this, **`x`** 和 **`y`** denot the abscissa and ordinate of the pellet, with initial values of 100 and 0, respectively. **`v`** represents the velocity of the pellet, and the initial value is 0. **`g`** represents the acceleration of gravity, the initial value is 0.1.

Next, in function **`setup()`** ,we can see the following code:

```jsx
function setup() {
  createCanvas(400, 400);
  background(0);
}
```

In this code, first use **`createCanvas()`** function to create a 400 x 400 pixel canvas then used function **`background()`** set the canvas's background to black.

Next, in function **`draw()`** ,we can see the following code:

```jsx
function draw() {
  fill(255);
  ellipse(x, y, 50, 50); // Draw the ball
  v += g; // update velocity
  y += v; // update position
  if (y > height) { // If the ball lands
    y = height; // Set the ordinate of the ball to the ground height
    v = -v; // Bounce of the ball
  }
}
```

In this code, first use function **`fill()`** set the fill color of the ball to white then use function **`ellipse()`** to draw the ball. Two arguments to the function **`ellipse()`** :The first and second parameters represent the abscissa and ordinate of the ball, respectively. Since these two variables are defined earlier, they can be directly represented by **`x`** and **`y`**. The third and fourth parameters represent the width and height of the pellet, respectively, here set to 50 pixels.

And then there's this line in the code:

```jsx
v += g; // update velocity
```

This line of code that USES the plus operator（**`+=`**, its role is to **`v`** the value of a variable with **`g`** the value of a variable, and the results will be assigned to **`v`** variables.  In other words, this line of code updates the speed of the ball.

And then there's this line in the code:

```jsx
y += v; // update position
```

This line of code that USES the plus operator （**`+=`**）, its role is to **`y`** the value of a variable with **`v`** the value of a variable, and the results will be assigned to variables **`y`** . That is, this line of code updates the position of the ball.

Finally, there is a conditional statement in the code:

```jsx
if (y > height) { // If the ball lands
  y = height; // Set the ordinate of the ball to the ground height
  v = -v; // Bounce of the ball
}
```

This conditional statement determines whether the ordinate of the ball is greater than the height of the canvas. If so, the ball has already landed.

In this case, the code executes two statements:

- The ordinate of the ball was set to the height of the canvas so that the ball landed on the ground.
- The velocity of the pellet was set to the opposite value so that the pellet could bounce.

With this code, we simulate the free-fall motion of the ball.