# Gachapon Machine Discord Bot

## Introduction 
In my free time I have often been involved in both playing in and running online text based RPG campaigns, which often include a system for players to spent in game currency and receive random items much like Japanese Gachapon machines. Typically this process involves a lot of work for the game masters in managing large spreadsheets of items and manually randomly selecting which items players had won from the machine. To reduce the amount of work and time game masters would be required to put into this mechanic, and also prevent players having to wait for game masters who may be busy to come online and give them items, I decided to write a Discord bot which would be able to both store and randomly distribute items added to it. 

[Discord](https://discordapp.com/) is a chat application that supports the addition of 'bots' to its group chats, which can aid the running of the server depending on what they are programmed to do. At the time of this project, all campaigns I joined were hosted on Discord, so adding the gachapon functionality to Discord was the natural solution. 

The bot was named 'Mowtron', after the NPC in the game in charge of the shop.

## Technologies Used
Though Discord bots can be written in a number of languages, Mowtron was written using Node.js. Node.js was chosen because of my basic knowledge of Javascript that I wished to develop further, along with a module for interacting with Discord's API ([discord.js](https://discord.js.org/#/) already existing that would allow straightforward completion of all tasks I wanted.  

Using Node.js also allowed me to make use of [Sequelize](https://sequelize.readthedocs.io/en/v3/) along with SQLite3, which would allow me to write database code essentially as I would write Javascript. As a database was the obvious choice for managing a large collection of items and their links to players, for me a simple way of creating and using a database through Mowtron was a high priority in choosing technologies to use. 

To allow Mowtron to be online for use even when the game masters are busy, the bot is currently hosted on [Glitch](https://glitch.com/). 

## Implementation
The required features for Mowtron were as follows:
* Manage a unique amount of currency for each player, with the ability for game masters to grant players more.
* Manage a complete list of all items in the gachapon machine, and complete lists of all items won by which players. 
* Allow players to spend any number of coins (within their balance) to win that number of items from the machine, deducting their currency appropriately. 
* Keep item rolls by players private so character inventories are kept secret from other players. 
* Allow game masters to still oversee the general state of items: game masters should be able to see all items still in the machine, all items owned by any given player, and any given player's balance. 
* Add new items into the machine at any given point.

To achieve all of these features, the database was designed with four tables: 
* **Characters:**  Keeps the user ID for each player in the server and their currency balance.
* **Item Pool:** Stores the items not yet won by any player; those still in the machine. Items are registered with a name and a description. 
* **Items Owned:** Stores the items that have been won by a player and therefore removed from the machine. These items still need to be in the database for a player's owned items to be viewed, but not kept within Item Pool, so exist within their own table. 
* **User Items:** The relationship table between characters and the owned items, linking the user and item ids. This table allows for viewing which characters own which items. 

Mowtron works via the input of user commands, which must be prefixed by 'm!' to prevent processing time being spent on parsing every single message sent in a large server. When a correctly prefixed message is registered Mowtron then performs argument parsing to work with the database correctly, for example incrementing the currency for the username given or selecting the given number of random items.

To both allow game masters to have a view of the full machine state and prevent players absuing the system by giving themselves extra currency or peeking into other player's inventories, Mowtron makes use of Discord's ability to assign users different roles within the chat. Through applying 'game master' and 'player' roles within the server, Mowtron can restrict certain commands and functionality to use only by game masters, with a warning provided for players who try. Use of roles also ties in with keeping player inventories private but allowing game masters to monitor Mowtron's use. When players win an item the result is privately messaged to them, but the result can also be sent publically to an output channel only those with the 'game master' role can view. 

## Results and What Was Learned 
After three weeks of planning and development an initial version of Mowtron was deployed in the campaign's Discord server for stress testing before the game began, since so far all testing had only been done in a server with one other person (myself). All 15 game masters and players were given the oppertunity to try using Mowtron to add and win dummy items simultaneously. Overall the reaction to Mowtron was overwhemingly positive, with the only negative response to be acted upon regarding the lack of feedback to mistakes being made in entering commands. Mowtron was updated with error messages for incorrectly used commands, as well as beginning to accept often seen typos of commonly seen commands (for example, typing 'm!item' instead of 'm!items'). 

Developing Mowtron helped improve my Javascript and database skills, along with being my first experience using Node.js and working on an application to be hosted elsewhere. 


## Usage Examples
Examples will be uploaded when the game begins and Mowtron is in active use. 

