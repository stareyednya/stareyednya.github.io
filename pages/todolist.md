# To-Do List Mod for Stardew Valley

## Demo
![To Do List Demo](https://66.media.tumblr.com/604283d89bf0a2e49e6af43ab1403fd6/tumblr_inline_ozbqd2QV6P1qdv35o_1280.gif)

## Introduction 
'Stardew Valley' is a farming simulator game originally developed by ConcernedApe which has since grown an active modding community. During my time with the game I noticed I was having trouble remembering every task I planned to do inbetween play sessions- and this was not a trait unique to myself when I mentioned it to others. This became the motivation for the development of my To-Do List mod, which functions as an editable task list in game which stores player notes inbetween play sessions. 

## Results and What Was Learned
To Do List was released as a public mod via Nexus Mods on the 12th November 2017. Since then, at the time of writing this page, the mod has recieved over 220 endorsements and over 7000 downloads. It is #33 for All Time for the catagory User Interface Mods out of 125 and #28 for All Time for the catagory Gameplay Mechanic Mods out of 82. To Do List functions on both Windows and Linux and with keyboard control and controller support, both implemented and tested by myself.

Developing this mod was my first experience programming in C# and as a result taught me the basics of the language. I also gained experience working with an API not developed or editable by myself in order to be able to implement the mod within the game via the use of SMAPI. Similarly to understand how Stardew Valley implements assets used such as the task panels and the text box input, I had to read and understand the original game's code. 

## Technologies Used
Stardew Valley was originally written in C#, so my mod was also written in the same language. I also made use of the open source modding API for Stardew Valley, [SMAPI by Pathoschild](https://github.com/Pathoschild/SMAPI), which allows for mods to be loaded into the game and enables cross compatibility. 

## Implementation 
* Provides the player with a panel of their noted tasks and a text box through which they can add additional tasks in their own words.
* A maximum number of tasks displayed on each page which the player can flip through, newer tasks first. 
* Clicking on a task marks it as complete and removes it from the list, moving up all tasks below. 
* Each save file within the game has its own individual task list. 
* A number of configuration options for the player to use the mod as they wish: 
  * Changable hotkey with which the menu is opened. 
  * A choice of font type and size for accessibility. 
  * Choose to automatically open the task list on save load for an instant reminder. 
* All assets used by the mod are those used by Stardew Valley itself, making the mod look a natural part of the game. 
* The size of the task list responds to the screen size. 
