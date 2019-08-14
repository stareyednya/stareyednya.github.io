# A Turn Based RPG Combat System Based On Timed Hits

## Introduction
For this project I wanted to experiment with creating a traditional turn based RPG combat system between a player party and a group of enemies. I also wanted to add more user interaction for each battle turn rather than just clicking through menus, so aimed to base attack mechanics around a simple 'timed hits' system. Timed hits add a type of quick time event to each attack, where the player can deal more damage with their own attack or reduce the damage caused by n enemy with a well timed button press. A well known example of this system is the Mario and Luigi RPG series. 

## Implementation 
The battle scene was created in the Unity game engine in the C# programming language. The demo scene features:
* Player and enemy units with battle stats, including HP for ending the battle when one party is reduced to 0, and Speed for deciding the order units can move in. 
* The player can select which enemy to attack with a moveable cursor. Enemy units move autonomously to complete their turn. 
* The battle ends when either all enemies are defeated or the player is defeated.
* All units have animations for idle stance, their attacks, and being hit. The player also animates on defence. 
* Achieved damage and any multipliers are displayed on hit.

## Timed Hits System
Damage caused by and done to the player can gain an additional multiplier depending on the timing of the player pressing space during the damaging part of the attack, split into three possible ratings:
* Critical: when the player hits at the peak of the attack, such as when the warrior's spear glows in his jab attck. The player's attack doubles in damage, or the damage done to the player halves. 
* Good: when the player hits a few frames either side of the critical point. The player's attack damage is multiplied by 1.5, or the damage done to the player is reduced by x0.75. 
* Okay: the player fails to hit in time, and no bonuses are applied.

To aim to keep the same frame based timing, the timing windows for each hit rating are based on the normalised time of the animations themselves (for attack animations that only play once, such as the jab attack), or account for the current position of the battle unit moving in its attack (for animations that loop, such as the bat's spin attack). 

## Modular Attack System 
To try and prevent the need to hardcode multiple complex attacks that may share similar elements, attack steps are constructed from multiple prefabs known as 'moves'. Each move stores the next step in the attack, and each move reports when its action has been completed. When all moves in the attack have been completed, the turn system advances to the next unit. Constructing each attack from these 'move' prefabs was benefical in preventing the amount of reused code in hardcoding attacks, and allowed for the easy reuse of attacks and their steps: the jab attack used by both the player unit and the reptile soldier consists of the same prefab simply dropped into their list of possible attacks, and all attacks share the steps of moving to and from their target.

## Results and What Was Learnt 
A demonstration of the completed battle scene can be seen in the video at the end of this page.

As all previous games completed by myself relied almost completely on player control within real time events, implementing a turn based system provided more experience with programming contained enemy behaviour using existing systems within the project, such as those used for moving and applying statistics to the player. This project also allowed me to design and implement new kinds of game programming logic I hadn't previously, such as the logic for determining the order of turns between all units in the battle and ensuring no turn actions overlap before completion. 

Avoiding the hardcoding of all attacks in favour of developing the modular attack system was an interesting exercise that proved useful in quickly setting up and expanding on attacks, and I can easily see how creating such generic tools or templates could speed up work in the future. 

## Improvements
While I am pleased with what I managed to achieve in this Unity experiment in the time I allocated to myself for this project, I would definitely have liked to expand what was included within the battle system with more time:

* I would have liked to include more types of attack for both players and enemies formed of much different types of action, such as a magic attack with a projectile moving towards the target instead of the unit approaching that could be jumped over to avoid damage on a timed press, or a ranged attack making use of a UI target to hit on time. 
* Currently each unit only has one possible attack, so a system where the player can select from a menu and an enemy can randomly choose 
an attack to use from a choice of multiple could be implemented for variety in the battle.
* There are currently no sound or other visual effects. The attack move prefabs already include support for multiple next actions being fired, either at the end of the action or as soon as the current action begins. This feature could be made use of to play extra effects as the action progresses.
* Additional UI would help provide battle information, such as a health bar for the player.

I would also like to experiment with making the entire battle system more generic. Currently each attack is responsible for its own timing of the player input, which started to become messier when not dealing directly with a player's own attack. It would likely be much cleaner to have a central 'Hit Timer' component to activate whenever an action needed to be timed, which could register the timing for any hit and the units currently in question could simply retrieve the information from. The enemies in the encounter are also currently hardcoded in: for this battle system to become a scene that could be reused throughout an RPG game for any possible combination of encounters, a system to load in chosen or random enemies would be needed.

## Video 
All art assets seen are from the [Superpowers Assets Packs by Pixel-boy.](https://github.com/sparklinlabs/superpowers-asset-packs)

<iframe width="560" height="315" src="https://www.youtube.com/embed/FaRleG1p6-w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
