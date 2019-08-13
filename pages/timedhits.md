# A Turn Based RPG Combat System Based On Timed Hits

## Introduction
For this project I wanted to experiment with creating a traditional turn based RPG combat system between a player party and a group of enemies. I also wanted to add more user interaction for each battle turn rather than just clicking through menus, so aimed to base attack mechanics around a simple 'timed hits' system. Timed hits add a type of quick time event to each attack, where the player can deal more damage with their own attack or reduce the damage caused by n enemy with a well timed button press. A well known example of this system is the Mario and Luigi RPG series. 

## Implementation 
The battle scene was created in the Unity game engine in the C# programming language. The demo scene features:
* Player and enemy units with battle stats, including HP for ending the battle when one party is reduced to 0, and Speed for deciding the order units can move in. 
* The player can select which enemy to attack with a moveable cursor. Enemy units move autonomously to complete their turn. 
* The battle ends when either all enemies are defeated or the player is defeated.
* All units have animations for idle stance, their attacks, and being hit. The player also animates on defence. 

## Timed Hits System
Damage caused by and done to the player can gain an additional multiplier depending on the timing of the player pressing space during the damaging part of the attack, split into three possible ratings:
* Critical: when the player hits at the peak of the attack, such as when the warrior's spear glows in his jab attck. The player's attack doubles in damage, or the damage done to the player halves. 
* Good: when the player hits a few frames either side of the critical point. The player's attack damage is multiplied by 1.5, or the damage done to the player is reduced by x0.75. 
* Okay: the player fails to hit in time, and no bonuses are applied.

To aim to keep the same frame based timing, the timing windows for each hit rating are based on the normalised time of the animations themselves (for attack animations that only play once, such as the jab attack), or account for the current position of the battle unit moving in its attack (for animations that loop, such as the bat enemy's spin attack). 

## Modular Attack System 
To try and prevent the need to hardcode multiple attacks that may have similar elements, att
