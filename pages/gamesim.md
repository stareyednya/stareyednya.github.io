# Stage 3 Gaming Simulations

# Result 
[TO COME]

# Introduction 
In this coursework I was given the basic framework of a 2D arcade game and tasked with completing its physics engine and AI. Gameplay consisted of the player navigating a robot around a map to pick up and lead 'Collectable Robots' back to a base to score points. Collectibles could also apply bonuses such as an increase in movement speed. Enemy robots were present on the map that would patrol, chase the player, and guard collectables to add difficulty.

Programming was entirely C++, with the use of a data file to load map tiles from. 

# What Was Learnt
This project really highlighted to me the importance of optimising physics engine calculations such that the game can continue to handle increasing amounts of entities without noticable lag, especially important in calculations relying on time. I also considered methods to reduce this number of entities to manage in the first place, such as combining individual wall tile colliders. The importance of appropriate data structures was also made clear as traversing these can be a timesink.  

# Implementation
Included physics elements:

* __Newtonian Physics__: the player, enemy robots and lasers all moved by the application of Newtonian dynamics. My physics engine made use of semi-implicit Euler integration to manipulate derivatives with consideration of the entity mass. 
* Springs: spring joints were used to create the chain of collectables to follow behind the player. 
* __Collision Detection__: I included two kinds of collision volumes, Spheres for all robots and lasers and Axis-Aligned Bounding Boxes for the walls and buildings. The engine first performs a sort and sweep broadphase, then completes a narrowphase for intersection of these volumes. 
* __Collision Resolution__: resolution by projection is used to seperate overlapping sprites, for instance the enemy robots. Resolution by the calculation of impulse is used to allow entities to bounce off each other. 
* __Collision Accleration__: along with sort and sweep, I further accelerated collision testing by dividing objects into static and dynamic to prevent unnecessary calculations for immobile objects.
* To allow __determination of which specific entities collided to produce gameplay effects__ (for example a laser hitting the player), I included a tagging system to register certain rigid bodies as specific entity types and gave each collision a OnCollision function. In this function, tags would be checked and relative event flags set to indiciate certain gameplay effects to the main game loop. This was helpful in separating the physics engine calculations from the game for a general purpose engine since the engine wouldn't be set to know this game's robots, lasers etc. 

Included AI elements:
* Enemy robot decisions were handled with the use of a __finite state machine__ to switch between patrolling, chasing the player, and guarding a special collectable when on the board. 
* __Pathfinding__: A* pathfinding is used to move the enemy robots to their chosen target (determined by the state machine). I took care to try and avoid all enemy robots following the same path or overlapping to get stuck on each other by marking which tiles on the map had already been chosen as targets by other enemies. The enemies also recalculate their path should they become stuck on a wall. 
* __Flocking:__ for an attractive pause screen, Reynold's BOIDs was used to make collectibles fly around the screen. Cohesion, separation and alignment rules are applied along with a tendancy to avoid collectibles of different colours. Should a flock leave the viewable screen, they wrap around to the other side. 


# Possible Improvements
A restructure of the collision volume handling could allow for a more centralised collision detection system with less repeated code. The project can also be further extended with the integration of additional gameplay effects based on the physics engine calculations. 


