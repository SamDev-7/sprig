# Welcome to Sprig!!!

You found the tutorial! 🎉  

## READ ME FIRST❗

**To run your game, hit the "Run" button in the top right of the editor.** *You can also use the `shift + enter` shortcut.*  
**Click the "Toolkit" tab at the top of this panel to discover your toolkit.**  

Sprig games are made in [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript). The toolkit contains documentation about Sprig functions and examples that you can reference for Sprig games.

In this tutorial, you will create a Sokoban, or a push box puzzle game.  
The objective is to push the purple boxes onto all of the green goals.  
Tip: Press `j` to reset the current level if you get stuck.

The game is incomplete and needs YOUR help! Solve the series of steps to finish the game.  
To solve each step, you'll have to edit the code. The code for this game is to the left.

There are hints and solutions along the way. Don't be afraid to use hints, but be sure to try it yourself before looking at the solution.  
**If you get really stuck, you can always ask for help in the `#sprig` channel on the [Hack Club Slack](https://hackclub.com/slack).**

Wahoo! Let's get started! 🌠

## Step 1

Try moving the character around with the `w`, `a`, `s`, and `d` keys. You'll notice that the player can only move down and right.  
**You'll need to add controls for the player to move up and left, use `w` and `a` as inputs.**

<details>
<summary>Stuck? Show Hint.</summary>

Take a look at how the down and right movement is implemented. It should be very similar to that.
</details>

<details>
<summary>I've tried my best. Show Solution.</summary>

Sprig's `onInput` functions are used to detect when a input is given. We can see that there are two `onInput` functions for the keys `s` and `d`.  

We'll need to add two more for the keys `w` and `a`.  

```js
onInput("w", function() {
  getFirst(player).y -= 1
});

onInput("a", function() {
  getFirst(player).x -= 1;
});
```

Note that the `y` and `x` values are to be subtracted (`-=`) instead of added (`+=`) because we are moving up and left, respectively. In most 2D game engines, like Sprig, decreasing the Y value moves the player up.
</details>

## Step 2

We cannot push the purple boxes to advance to the next level.  
**You'll have to make the purple boxes pushable.**

<details>
<summary>Stuck? Show Hint.</summary>

Check the toolkit for `setPushables`!
</details>

<details>
<summary>I've tried my best. Show Solution.</summary>

The `setPushables` function allows us to define which sprites can push other specific sprites. In our case, we want the player to be able to push boxes.  

Part of `setPushables` has already been written, we'll have to modify it.

```js
setPushables({
  [player]: [ box ]
});
```

Note that everything in `setPushables` has to be a solid. You can set a sprite as solid with `setSolids` (check the toolkit).  
We don't have to worry about this as it already has been done for us.
</details>

## Step 3

Yay, we can get to the next level now! When you reach level 3, the wall blocks your path and there is no way to pass it.
**Edit the third level to make it solvable and add some new levels.**

<details>
<summary>Stuck? Show Hint.</summary>

Check the comments, are there anything that describes the game's levels?
</details>

<details>
<summary>I've tried my best. Show Solution.</summary>

In our game, the `levels` variable stores an [array](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Arrays) of levels. Each level is a Sprig `map`. By clicking on the green `map` text, you can enter the level editor.

We'll need to edit the third level to make it solvable, remove a few walls.
</details>

## Step 4

Great, we can now reach level 4. However, we cannot push the purple boxes to advance to the next level. This is because the boxes are blocked by other boxes.  
**To fix this, allow boxes to push boxes.**

<details>
<summary>Stuck? Show Hint.</summary>

Remember how you made something pushable in step 2? You'll need to do something similar.
</details>

<details>
<summary>I've tried my best. Show Solution.</summary>

Similar to how we made the player push boxes, we'll need to make boxes push boxes.  

We'll have to modify `setPushables` again.

```js
setPushables({
  [player]: [ box ],
  [box]: [ box ]
});
```

The `setPushables` function takes in an [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects) which links sprites (listed with an [array](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Arrays)) to other sprites (which are also listed using an array) that it can push using a colon. Each pair is separated by a comma.
</details>

## Step 5

You're almost there, but the game is still missing something.  
**Add sound effects when you move.**

<details>
<summary>Stuck? Show Hint.</summary>

Check the "Toolkit" tab for information on tunes, music, and sound effects.
</details>

<details>
<summary>I've tried my best. Show Solution.</summary>

This is a little bit more complicated. We first have to create a Sprig tune, then figure out a way to play it.  

Creating a tune works as follows:

```js
const tune = tune`...`;
```

Click the green `tune` text to enter the tune editor. Create something of your own!

After creating a tune, we can play it using Sprig's `playTune` function.  

```js
playTune(tune);
```

But, we only want to play the tune every time the player moves.  
What is something that related to player movement?  
Every time the user presses `w`, `a`, `s`, or `d`, the player moves.

We can put the `playTune` function inside the `onInput` function. The result should be something like this.

```js
onInput("w", function() {
  getFirst(player).y -= 1
  playTune(tune);
});

onInput("a", function() {
  getFirst(player).x -= 1;
  playTune(tune);
});

onInput("s", function() {
  getFirst(player).y += 1; // positive y is downwards
  playTune(tune);
});

onInput("d", function() {
  getFirst(player).x += 1;
  playTune(tune);
});
```

</details>

## Step 6

Congratulations! You just made a game. 🥳
**Now solve the puzzle you just created! Make sure that nothing is broken.**

## I'm done, now what?

Congrats! Now make your own game! Try:

- adding two players.
- leaving a trail as you move.
- having different boxes and goal types.
- come up with your own mechanic!

**If you need help, remember that the toolkit is there for you. You can also ask in the `#sprig` channel in the [Hack Club Slack](https://hackclub.com/slack/).**
