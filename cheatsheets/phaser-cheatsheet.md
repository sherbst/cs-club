# Phaser 3 and JavaScript Cheatsheet

This cheatsheet provides tips for using both JavaScript and Phaser 3.

# JavaScript

JavaScript is a scripting language that is popular in the browswer. It is largely the only language supported by browsers for scripting purposes on websites. Some tips on the usage of JS are written below.

## Types

JS supports several "primitive" types.

1. Number: `1`, `3.14`, `10e2`, etc...`
2. String: `"string here"`
3. Boolean: `true` or `false`

## Variables

Variables are created one of 2 main ways:

1. Constants

Can not be modified.

```js
const age = 10;
const name = "Johnny";
const isMale = true;
```

1. `let` variables

_Can_ be modified.

```js
let name = "Johnny";
name = "James";
name = "Jeff";
```

Variables can also be created with `var`, but it is not reccomended to do so.

## Functions

Functions are used to create a piece of code that can be re-ran on demand.

You create a function like so (`functionName` could be any valid name):

```js
function functionName() {
  // Any code that should be ran goes here
}
```

You then make a function run like so:

```js
functionName();
```

# Phaser 3

## Template

A boilerplate Codesandbox template for a Phaser 3 game can be found [here](https://codesandbox.io/s/phaser-template-6o3wy?file=/assets/js/index.js).

## Examples

1. [Pong](https://codesandbox.io/s/pong-201zq?file=/assets/js/index.js)

## Lifecycle Methods

1. `preload()`: Runs once at the very start of your game. Should be used to load assets (images, sounds, etc...).
2. `create()`: Runs once at the start of your game (after `preload()`). Should be used to create/modify sprites, create colliders, etc...
3. `update()`: Runs infinitely until the end of the game. Should be used to update anything that needs to be constantly updated in the game (score, positions, velocity, etc...)

## Loading Images

```js
this.load.image("ball", "assets/img/ball.png");
```

## Creating Sprites

```js
this.ball = this.physics.add.sprite(250, 250, "ball");
```

## Modifying Sprites

```js
this.ball.setScale(0.05);
this.ball.setCollideWorldBounds(true);
this.ball.body.bounce.set(1);
this.ball.setMaxVelocity(400);
```

## Create a Collider

First, create the collider in `create()` (`onBallCollide` can be named something else, and you can use different game objects other than `this.ball` and `this.paddleL`):

```js
this.physics.add.collider(
  this.ball,
  this.paddleL,
  onBallCollide,
  undefined,
  this
);
```

Then define the `onBallCollide()` function. Note that this should go at the very bottom of the code (not in any lifecyle method):

```js
function onBallCollide() {
  // Any code in here will run when the two object specified above collide
}
```

## Keyboard Input

In the `create()` method:

```js
this.cursor = this.input.keyboard.createCursorKeys();
// or, if you want custom keys:
this.wasdKeys = this.input.keyboard.addKeys("w,s,a,d");
```

In the `update()` method get user input with:

```js
this.cursor.up.isDown; // true, if the up key is pressed
this.wasdKeys.w.isDown; // true, if the w key is pressed
```
