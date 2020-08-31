+++
categories = ["web-dev", "coursework"]
coders = []
date = 2019-02-14T00:00:00Z
description = "Creating a reusable component from a p5 Sketch"
github = ["https://github.com/samrobbins85/Programming-P5-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593512330/p5js_hcoqdy.svg"
site = "https://p5-programming.now.sh/"
title = "p5 Component"
type = ""
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793272/logos/logos_javascript_adj1dx.svg"
name = "JavaScript"
url = "https://www.ecma-international.org/memento/tc39.htm"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593512330/p5js_hcoqdy.svg"
name = "p5"
url = "https://p5js.org/"

+++
In this coursework we were to take a p5 sketch from [https://www.openprocessing.org/](https://www.openprocessing.org/ "https://www.openprocessing.org/") and adapt it into a reusable component. For this I used the sketch [https://www.openprocessing.org/sketch/429506](https://www.openprocessing.org/sketch/429506 "https://www.openprocessing.org/sketch/429506"). It looks like this:

![Image of sketch](https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593525155/2020-06-30_14-52_j7lpkb.png)

## Running

This only needs an internet connection to request the various libraries involved, it can be ran by just opening the HTML file in your browser

## Example functions

### Setup
```js
function setup() {
  createCanvas(windowWidth, windowHeight);
  rectMode(CENTER);
  textAlign(CENTER);
  textSize(14);
  colorMode(HSB);
}
```

### Draw

```js
function draw() {
  let b = new shape();
  b.background_colour = background_colour;
  b.speed = speed;
  b.offset = offset;
  b.value1 = value1;
  b.value2 = value2;
  b.draw();
}
```

## Parameters

The parameters for the constructor of the class shape are as follows:

| Parameter         | Type    | Min | Max | Description                                |
| ----------------- | ------- | --- | --- | ------------------------------------------ |
| background_colour | Integer | 0   | 360 | The colour of the background of the sketch |
| speed             | Integer | 0   | N/A | The speed at which the shape oscillates    |
| offset            | Integer | 0   | 90  | The offset between the squares             |
| value1            | Integer | 0   | 360 | The minimum colour of the shape            |
| value2            | Integer | 0   | 360 | The maximum colour of the shape            |

All these parameters then have methods in the form of getters and setters in order to verify the data being passed is in the correct format and range.

value1 should be less than value2, but if this is not true, the definitions of value1 and value2 will be swapped so that the sketch still works.

There are then three functions:

- `draw` - This performs all the drawing of the shape
- `mouseDragged` - This changes the values of the variables twist and count when the mouse is clicked and dragged
- `constructor` - This creates and initialises the object within the class shape

## Explanation of example

The example allows you to control all of the parameters for the constructor shape.

- The background colour slider controls the parameter background_colour
- The speed slider controls the parameter speed
- The offset sider controls the parameter speed
- The colour range slider has two sliders on it, the left hand one controlling value 1, and the right hand one controlling value 2

The example uses the variable b to draw the shape