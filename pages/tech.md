# Stage 4 Advanced Game Technologies 

## Video 
Enable captions for descriptions of each feature as they are shown.
<iframe width="560" height="315" src="https://www.youtube.com/embed/UezDHAB25gA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

"An excellent coursework. The collision detection is done well...the use of collision layers for automatic handling of which objects can react are a neat touch. The additions made are logical and make for a very efficient broadphase. The state machine is well thought out and integrated nicely with the pathfinding code. The networking is very nicely done." - Dr Rich Davison 

## Introduction
The aim of this project was to create a simple 3D game where the player would control a goose out to steal items, similar to Untitled Goose Game. The game would be created using a framework provided by Newcastle University to implement physics, collision detection/response, AI and networking game components within. 

## What Was Learnt 
Though I had completed similar projects to this before in adding physics and AI to a game, this was my first instance of doing so in 3D, and it was interesting to see the differences in implementation of similar ideas with the change from 2D to 3D (such as using A* on a generated navigation grid rather than map tiles and collisions accounting for extra axes and the use of OBBs). This was also my first try at making use of networking which brought interesting considerations about creating custom packets and sending the minimum amount of information needed. 

## Implementation
My finished game contained a number of features as part of its game engine:

* __Raycasting__: used to help determine if the goose is close enough to an item to pick it up, and prevent infinite jump by checking distance from the floor.
* __Application of Forces__: objects move according to forces applied within the world, using linear and angular motion integrated with Semi-Implicit Euler. 
* __Collision Detection__: the physics engine can detect and handle collisions between AABB/AABB, Sphere/Sphere, AABB/Sphere, and Sphere/OBB. Inspired by Unity's collision layer matrix, objects can be given a collision layer to be in, and detecting collisions between objects on pairs of layers can be disabled. This helped prevent issues with intersecting the simple geometric meshes to create world objects, and allows for interactions such as the goose hiding in plants where AI cannot go. Events occur based on collisions, such as dropping held items onto the island for points and to reset the AI.
* __Collision Resolution__: the physics engine allows objects to differentiate between using one of two types of collision resolution depending on the intended effect: resolution by impulse and the penalty method in the form of springs. Objects can be tagged as having both resolution types allowing for different interactions, such as the unique effect of the goose bobbing on the water versus walking on the floor. 
* __Collision Acceleration__: collision detection is optimised with a broadphase dividing objects into static and dynamic for use with quadtrees. One static object quadtree is built on beginning a new game which dynamic objects in their quadtree region are tested against. Objects are also put to sleep if their position hasn't changed drastically over a number of frames, and are also skipped over in collision detection. 
* __AI__: NPC characters act according to a finite state machine based on whether the goose is close and has stolen or returned an item. A* pathfinding is used to cover large distances to chase the goose or return to their area. 
* __Menus__: the game contains a menu system based on a pushdown automata system. The player can move from a main menu to a single player or networked game instance, which can then be paused and unpaused to return to the main game state and will refresh the state stack after moving to a game over state. 
* __Networking__: Players can choose between running a single player game, or having their game play as a server or client over local host. At any time a client player can request a highscore table from the server which will send the information for the client to display. The server controls a unique NPC which will update for all clients depending on the player being chased and can also update player geese by receiving player directional input. Items picked up by a player will update for all connected clients through the server making use of consistent object IDs to identify the item one player is trying to pick up and signal it should be assigned to that goose. 
* __Level creation__ is based on a text file loaded in at the beginning of the game depending on whether single or multiplayer is picked, making use of symbols to spawn objects in the relative spaces. This allows for quick level design and also forming a navigation grid around symbols marked as walkable for A*. 

## Possible Improvements
Though information is sent between client and server to update object positions for all connected games, the game in its submitted form still only supports and shows one player goose. It would be good to extend the framework left in place (starting islands being assigned to player geese to store points, the server sending NPC and item updates to all clients) to add another goose to a networked game.
