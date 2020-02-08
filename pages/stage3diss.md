# Dissertation Stage 3: Performance Analysis of Procedural Generation Techniques for Roguelike Game Levels

## Examples
All art assets seen in the project come from Unity's 2D Roguelike tutorial (all floor and wall tiles) and Hyperluminal Games (keys and locks).

![Maze With Rooms](/images/mwr.png)
![BSP Tree](/images/bsp%20tree.png)
![Parameters](/images/parameters.png)

## Introduction 
For my Stage 3 Dissertation, I wanted to complete an algorithm-based project which would also allow me to become more familiar with using a commercial game engine. The final project combined this thought along with a personal interest in the Roguelike genre and random generation of continually different levels, leading to great enjoyment in the work. 

The project's aim was to implement two differing algorithms for procedurally generating a 'traditional' roguelike dungeon map (similar to those seen in [Rogue](https://upload.wikimedia.org/wikipedia/commons/1/17/Rogue_Screen_Shot_CAR.PNG)) within a game engine and compare their methods in terms of time taken, memory usage, and the playability of the result. The project also investigated the addition of gameplay elements to the map by creating locked rooms that required keys. 

## Technologies Used 
Unity game engine with C# programming. Unity's diagnostic profiler was also used for performance analysis.

## Results and What Was Learnt
Both algorithms were implemented successfully, and I found that between the two, the BSP Tree performed significantly faster by placing the largest elements (rooms) first where Maze with Rooms frequently had to scan the whole map. However space partioning required more memory use to hold the extra partition information.

During this project I learned a great deal about optimisation of loading time and memory usage within a game engine, with my performance analysis highlighting bottlenecks not previously considered to keep in mind for future game projects. This project was also my first introduction to A* pathfinding alongside considerations of what defined a 'good, winnable level', and my first completed project in the C# programming language. 

## Implementation 
For comparison purposes it first had to be decided which two algorithms would be implemented. I decided to choose two that differed in the order in which they drew the two identified main elements of a map: rooms and corridors. The two chosen were based on maze generation algorithms (['Maze with Rooms'](https://gist.github.com/timdetering/5e4f10d311db9991fa7330be701cabcc)) and Binary Space Partioning ([BSP Tree](http://www.roguebasin.com/index.php?title=Basic_BSP_Dungeon_generation)). These algorithms were then implemented in Unity; a challenging aspect of the project since both original implementations were not written to account for game engine objects.

The project also investigated different methods and locations of instantiating the game objects required to build the map once generated. This investigation was developed as I progressed through the project and learned more about the efficient use of a game engine in order to reduce loading times and memory usage in this area. 

To aid in testing all forms of map generation were implemented within the same Unity project as modules, allowing me to switch in and out which algorithm to use and which instantiation method. The user of my generator could also set parameters for the size of the final generated level and other qualities. 

For good placement of locked rooms and their keys I was required to write my own algorithm, which created a natural critical path through the map by placing the key for the second lock behind the first lock, the key for the third lock behind the second lock, etc. I included an A* pathfinder during this phase of generation to ensure that a key was not placed behind the lock it opened and created an unwinnable level.  


## Possible Improvements
While there was constant optimisation of how map tiles determined information about their neighbours for generation purposes throughout the project, the amount of times this has to be done could be likely further reduced with a restructure of how I represent and store tile information in the code, associating neighbour information within specific tiles instead of external searches being performed. 

Both algorithms could also be further refined to account for some edge cases spotted during testing such as BSP Tree not locking all possible entrances to a room. 

