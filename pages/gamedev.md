# Stage 3 Computer Games Development

## Introduction 
For this coursework I developed my own video game over the course of 4 months. I chose to produce 'Head Home': a 2D infinite runner where the player controls a lost cat and aims to traverse as many 'rooms' as possible before time runs out or all health is lost. The rooms are populated with obstacles and enemies to avoid, and the player can find items along the way to help clear a larger number of rooms. 

## Implementation
The game was developed in the Unity game engine in the C# programming language. Features of the game are:

* Random Room Generation: in each room the selection of enemies, their placement and number in the room, and the start time of their attacks is random, along with the number and placement of obstacles. I wrote my own room generation algorithm to ensure that the player would always be able to reach the exit by enforcing a maximum number of blocks on each room row, and enemies wouldn't be too clumped together by checking which tiles were already occupied by them and their attack ranges.
* Random Items: the selection offered to the player in each item room is random. Each item has an assigned rarity with a different percentage chance of appearing, and the item room generation wll determine the rarity of the item to be offered before selecting a random item from that rarity's pool. 
* Seed Functionality: all random generation for a run is based on one sequence of random numbers generated at the start of the session, allowing the same results to be gained from input of a seed value. 
* Item Types: the player can collect two kinds of items: passive items which adjust their stat boosts and attack types, and active items that can be used to alter the room of enemies and their attacks. All items can be seen in the video at the bottom of the page.
* Range of Enemy Types: 
  * 'Obstacle' enemies to make the player consider where to move to
  * Moving enemies using A* pathfinding to navigate to the player and attack them, some only 'awakened' when the player moves close
  * Enemies with magic attacks that attack certain tiles around them each cycle.
  * Enemies with magic attacks that target the player's current position, some with predictive shot. 
* Scoring System: players can earn points for the number of rooms cleared with a bonus for no damage taken and from defeating enemies. 
* An introductory cutscene and title screen. 
* A full tutorial.
* Four different game modes: 2 minute timer, 5 minutes, 10 minutes and endless mode. A hub world is used to changed between them. 
* Dynamic camera with Unity's Cinemachine to produce a transition effect between rooms. 
* Sound Effects: every scene comes with background music, and each movement, attack and item use uses sound effects. 

## Results and What Was Learnt
The completed game is playable online [here](https://eleanoot.github.io/HEADHOME/index.html) (works best on Mozilla Firefox due to bugs within Unity's WebGL export). 

This project was my first completed video game.

## Improvements

## Video
No art assets seen in the project are mine.

[![Head Home Item Showcase](http://img.youtube.com/vi/aAaEPwPSld8E/0.jpg)](http://www.youtube.com/watch?v=aAaEPwPSld8 "Head Home Item Showcase")
