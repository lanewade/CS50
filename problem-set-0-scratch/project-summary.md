# Problem Set 0 — Scratch

## Crab Grab

**Platform:** Scratch  
**Project Type:** Interactive game

Crab Grab is a small game I built for CS50 Problem Set 0. The player controls Shelly, collects Cheedos to increase the score, and avoids a moving banana hazard that removes points.

## Player Movement

Shelly is controlled with the arrow keys.

```text
when [left arrow] key pressed
    change x by -10

when [right arrow] key pressed
    change x by 10

when [up arrow] key pressed
    change y by 10

when [down arrow] key pressed
    change y by -10
```

## Game Start and Win Logic

Shelly returns to the center when the game begins. The game continuously checks the score and triggers the celebration sequence once the player reaches 5 points.

```text
when green flag clicked
    go to x: 0 y: 0

    forever
        if <Score > 4> then
            celebrate("BANANAS MAKE ME MAD")
            set Score to 0
            go to x: 0 y: 0
```

The instructions are also displayed when the game starts.

```text
when green flag clicked
    say "Use the arrow keys to grab 5 Cheedos!" for 5 seconds
```

## Cheedos Collection Logic

The score begins at 0 and the Cheedos spawn at a random position.

A collision check prevents the Cheedos from spawning directly on top of Shelly.

```text
when green flag clicked
    set Score to 0
    go to random position

    repeat until <not <touching Shelly?>>
        go to random position

    forever
        if <touching Shelly?> then
            start sound [yes]
            change Score by 1

            repeat until <not <touching Shelly?>>
                go to random position
```

This allows each collection to count once while also forcing the next Cheedos location to be somewhere Shelly is not already touching.

## Banana Hazard Logic

The banana starts by choosing a random direction and continuously moves around the stage.

```text
when green flag clicked
    point in direction (pick random 1 to 360)

    forever
        if <Score < 5> then
            move 5 steps
            if on edge, bounce

            if <touching Shelly?> then
                if <Score > 0> then
                    change Score by -1
                    start sound [STOP!]
                    wait until <not <touching Shelly?>>
```

The `Score > 0` check prevents the score from becoming negative.

The `wait until not touching Shelly` condition prevents one collision from rapidly removing several points.

Because the banana movement only runs while `Score < 5`, it stops moving during the celebration and begins moving again after the score resets to 0.

## Custom Celebration Block

I created a custom block that accepts a message as an input.

```text
define celebrate(message)
    change color effect by 25
    start sound [i did it, yay]
    say (message) for 3 seconds
    clear graphic effects
```

This lets the celebration behavior stay grouped together instead of repeating the same blocks throughout the program.

## Programming Concepts Used

- Event-driven input
- Variables and game state
- Forever loops
- Conditional statements
- Nested conditions
- Collision detection
- Randomization
- Input parameters
- Custom blocks
- State validation
- Audio and visual feedback
- Basic debugging and game-flow control
