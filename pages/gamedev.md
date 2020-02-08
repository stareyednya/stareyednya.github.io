# Stage 3 Computer Games Development

## Final Result
The completed game is playable online [here](https://eleanoot.github.io/HEADHOME/index.html) (works best on Mozilla Firefox due to bugs within Unity's WebGL export). The below videos showcase different aspects of the game:

Beginning of the game and tutorial:
<iframe width="560" height="315" src="https://www.youtube.com/embed/rwgube0nhwY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

One run of the game:
<iframe width="560" height="315" src="https://www.youtube.com/embed/KpccxtfeSKg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Item Showcase:
<iframe width="560" height="315" src="https://www.youtube.com/embed/aAaEPwPSld8" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

"The game plays very well... there are some very nice touches that really do make it feel polished. Technically the game presents a complete enviroment that satisfies the gaming requirements. - Dr Graham Morgan

## Introduction 
For this coursework I developed my own video game over the course of 4 months. I chose to produce 'Head Home': a 2D infinite runner where the player controls a lost cat and aims to traverse as many 'rooms' as possible before time runs out or all health is lost. The rooms are populated with obstacles and enemies to avoid, and the player can find items along the way to help clear a larger number of rooms. 

## What Was Learnt
This project was my first completed video game and as a result I learnt a lot about game development from both the use of a game engine and a player's perspective. I learnt new skills within Unity such as adding animation, applying different levels of collision detection and combining numerous elements into forming a connected game, as well as practicing use of external packages by working with their Cinemachine components. From a player perspective I also learnt to consider game design principles such as ensuring rooms were completable and the increasing challenge. 

## Implementation
The game was developed in the Unity game engine in the C# programming language. Features of the game are:

* **Random Room Generation:** in each room the selection of enemies, their placement and number in the room, and the start time of their attacks is random, along with the number and placement of obstacles. I wrote my own room generation algorithm to ensure that the player would always be able to reach the exit by enforcing a maximum number of blocks on each room row, and enemies wouldn't be too clumped together by checking which tiles were already occupied by them and their attack ranges.
* **Random Items:** the selection offered to the player in each item room is random. Each item has an assigned rarity with a different percentage chance of appearing, and the item room generation will determine the rarity of the item to be offered before selecting a random item from that rarity's pool. 
* **Seed Functionality:** all random generation for a run is based on one sequence of random numbers generated at the start of the session, allowing the same results to be gained from input of a seed value. 
* **Item Types:** the player can collect two kinds of items: passive items which adjust their stat boosts and attack types, and active items that can be used to alter the room of enemies and their attacks. All items can be seen in the video at the bottom of the page.
* **Range of Enemy Types:**
  * 'Obstacle' enemies to make the player consider where to move to
  * Moving enemies using A* pathfinding to navigate to the player and attack them, some only 'awakened' when the player moves close
  * Enemies with magic attacks that attack certain tiles around them each cycle.
  * Enemies with magic attacks that target the player's current position, some with predictive shot. 
* **Scoring System:** players can earn points for the number of rooms cleared with a bonus for no damage taken and from defeating enemies.
* **Animations:** Enemies, their attacks, and items all have animation. 
* **Increasing Difficulty:** the more rooms a player completes in a run, the more enemies will appear in following rooms. The number is randomly selected based on a graph function, with my own tweaking to ensure an appropriate beginning of the game challenge.
* **Beginning The Game:** An introductory cutscene, title screen, and full tutorial.
* **Four Different Game Modes:** 2 minute timer, 5 minutes, 10 minutes and endless mode. A hub world is used to changed between them. 
* **Dynamic Camera:** Unity's Cinemachine produces a transition effect between rooms. 
* **Sound Effects:** every scene comes with background music, and each movement, attack and item use uses sound effects. 
* **Debug Console:** an included command console that can be used for debugging by spawning enemies and items, changing player stats, and clearing the current room to speed up testing. 

## Improvements
WIth more time my algorithm for the natural spread of enemies and obstacles across the grid could be refined. The algorithm went through numerous versions during development and some edge cases remain where these entities will still be placed next to each other from this combination of implementations. A restructure would allow for a more optimised way of spreading entities, whether that came from cleaning the original code or even basing my implementation on another grid based method such as Conway's Game of Life. 

A number of polishing touches could also be added to provide extra immersion effects such as screenshake. The increasing difficulty could be adjusted to only allow the harder enemy variants to appear at higher numbered rooms. 

