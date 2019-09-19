# RPG Overworld Test

## Introduction 
With my continued interest in RPG mechanics and their storytelling, I was interested in putting together a small scene that could make use of a dialogue engine in order to show branching conversations between characters, as no previous game projects of mine had required any form of dialogue. This project then developed into a test of including several other typical game features I hadn't previously created: an inventory system, saving and loading a game's state between sessions, and a changing overworld (tying into remembering the game's state). 

## Technologies Used and Implementation
The RPG scene was created in the Unity game engine in the C# programming language, along with interpretation of the Yarn language (further described in the next section). 

Both the inventory and the save/load systems were original systems written by myself. For the inventory system, each object visible in the overworld that can be feasibly picked up is its own class of InventoryItem, with specific behaviour (such as the noise that plays when a vegetable is taken) further defined in their specific classes. The inventory manages a certain number of slots for these items, which can be displayed in an 'Inventory' submenu. 

Saving and loading makes use of Unity's Serialization and Deserialization to write the player's current state to disk. On pressing 'Save Game', a save object is created to serialize the player's current position in the world, their current inventory, the current status of all dialogue flags present in the scene (such as whether a certain quest has yet been started), and which items if any have been removed from the overworld. All data except the player's position required custom serialization to store their information, being based on my own structures that Unity has no way of automatically serializing. On loading of this game data, the overworld scene reloads itself and appropriately applys the data found in the save object, such as moving the player to the correct position and refilling their inventory. 

To create the changeable overworld, scene reloading on load of a save game uses an additive approach: the base scene is the town map without any takeable items, and each takeable item is contained within their own scene which is loaded on top of the base if the saved game state does not mark that item as having been removed. I chose this approach rather than a reverse direction, as loading the full scene with all items then searching for and deactivating those taken would have required much more careful management of item storage and identification in order to not accidentally remove the wrong one. 

## Working with Yarn Spinner
Dialogue inclusion made use of [Yarn Spinner](https://github.com/YarnSpinnerTool/YarnSpinner), a tool created by [Secret Lab](https://www.secretlab.com.au/) for easy creation of interactive dialogue for games. I chose to use a third party dialogue system rather than developing my own to gain practice working with and extending software not written by myself, and I chose Yarn Spinner specifically due to its intended integration being with C# and Unity. Yarn Spinner also provides a base not specific to any one type of game which I felt I could spring off easily, as opposed to a system specifically developed for a genre like visual novels. 

In including Yarn Spinner in my project, I made use of the standard features offered such as the displaying of the dialogue text and the structuring of a conversation around choosable options. To fulfil my project's scope however I built on top of the example classes given by Yarn Spinner for these basics. Below is a list of the Yarn Spinner functionality used and my extensions to them:

* Display of dialogue text character by character: I added the ability to speed up the dialogue by pressing any key, and added a typewriter sound effect to play for each character to provide the sound accurately no matter the length of dialogue.
* Sprites changing depending on NPC dialogue: Each NPC in my project was assigned a number of character portraits for different emotions, and I added a custom function to Yarn Spinner that could be read from the dialogue to set a UI portrait by specifying the character and emotion to show. 
* Dialogue flag variables being set within conversations: I wrote custom serialization for these Yarn values in order to allow the game to remember which NPCs had been visited and which dialogue flags had been set between game sessions. I also added the ability for Yarn Spinner to include variables set outside of the dialogue so conversations could account for changes in the world, such as an item being taken.

## Results and What Was Learned 

A demo of all features can be seen at the end of this page. 
At the end of the time I allowed myself for working on this project, the overworld scene contains these features: 
* A moveable player with an interaction radius for picking up items and talking to NPCs, and a dynamic camera that follows them around the world without ever leaving the boundary. 
* A dialogue system with branching paths depending on factors such as options chosen by the player within the conversation, whether the NPC has been talked to before, held inventory items and other actions in the world. 
* Additional dialogue functionality of skipping text, sound effects, and representing the character speaking by displayed portraits. 
* An overworld scene which can be changed between game states by including items to pick up, which won't be reloaded on the following game session. 
* An inventory system which adds, removes, and displays items acccordingly.
* A fully functional save and load system for the game state, keeping the player's current position, inventory, and triggered conversations between game sessions. 
* A main menu UI with submenus to be navigated through, with previous menus deactivating and reactivating as appropriate.

This project was my first attempt at implementing a number of typical game features such as saving the game and an inventory system, and in doing so I have learned a large amount about designing data structures to be used by both the player and the game in what their offered functionality should be and where it should be offered to neatly be accessed by the rest of the game. Saving and loading in particular as my first try at serialization was a challenging experience: as the project did not begin with save/load in mind, no implemented features accounted for later needing to be serialized, and a large amount had to be restructured. When next working on a project that will need to have its game state saved, I have learned to consider this fact first and structure the game around it rather than trying to tack it on as an afterthought. 

Through using Yarn Spinner I have also gained experience with including a third party system within my project and extending it to fit my project's needs. Though I specifically learnt Yarn Spinner, I now feel more confident in being able to understand and exttend third party code even where documentation regarding the specifics of what I want to do is lacking or nonexistent. 

## Improvements
Overall I am very happy with the results of this project and the fact that I managed to implement each feature I wanted to. I am particularly happy with the additions unique to my project game such as my extensions to Yarn Spinner and the custom serialization of my game's structures. However there are still features I would have liked to try add with more time or in any next similar project, or some small smoothings out to included features:

* There are a number of additions that could be made to the dialogue system to further differentiate parts to it, such as including different text effects for certain words (e.g. colours, shaking letters) or different text sound effects for different characters speaking. 
* While the additive scene loading to remove taken items from the world, there are some small but noticable stutters in the loading as each part is checked. An improvement to this could be to disguise the loading time with a transition screen of some kind, or to investigate Unity's asynchronous scene loading further to give the appearance of everything loading at once from the background. 
* Currently there is only one save file with a hardcoded name that is repeatedly overwritten and loaded. I would have liked to try including multiple save slots with user defined names for the player to choose between loading. 

## Video
Art assets used: 
* [Tiny RPG Town Envionment](https://assetstore.unity.com/packages/2d/environments/tiny-rpg-town-environment-88293) for the overworld map
* [Fantasy Wooden GUI](https://assetstore.unity.com/packages/2d/gui/fantasy-wooden-gui-free-103811) for the main menu and dialogue UI
* [Storyteller's MV Facesets](https://forums.rpgmakerweb.com/index.php?threads/storytellers-mv-facesets-updated-01-01-17-sf_people1_7.47069/) for the character portraits seen while talking

<iframe width="560" height="315" src="https://www.youtube.com/embed/cePCwuFSlRo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
