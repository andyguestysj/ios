---
title: Common Concepts
permalink: /docs/vocab-4/
---

## Player Interactions

Players interact in different ways in different games. In some games they barely interact at all, in others different players interact in different ways, for example Crew versus Imposters in Among Us.  

At the simplest level we can categorise player interaction as solitaire, competitive and co-operative, but is a simplification and the image below shows.  

<centre>        
    <img src="{{ "/assets/img/vocab/playerinteractions.png" | relative_url }}" alt="Different types of player interaction" class="img-responsive">
</centre>

## Objectives

Games can have almost any objective. Listed below are a few common ones.  

* **Capture**. Players have to avoid getting captured or killed while destroying some opponent properties (commonly some form of terrain or units).
* **Chase**. Players have to elude or catch an opponent.
* **Race**. Players have to reach a goal before anyone else does.
* **Alignment**. Players have to align their pieces in a spatial or conceptual configuration.
* **Rescue or Escape**. Players have to get some defined units or items to safety without being compromised.
* **Forbidden Act**. Players have to get the opponents to break the rules or to abandon a strategy.
* **Construction**. Players have to construct, maintain, or manage game objects.
* **Exploration**. Players have to explore unknown game areas.
* **Solution**. Players have to solve a problem or puzzle (sometimes before the opponents solve it).
* **Outwit**. Players have to gain and use knowledge to outwit their opponents.

## Procedures

Procedures are actions or methods of play allowed by the game’s rules. Categories of procedures include:  

* *Starting* (How the game is put into play)
* *Progression* (These are the ongoing procedures running during gameplay)
* *Special* (These are actions that are only available based on other elements and changes to the game state)
* *Resolving* (These actions bring your game to an end)

## Rules

These are the exact objects and concepts of the game; they are the building blocks of the game system. The rule set specifies everything a player *can* and *cannot* do.  The main purposes of the rules are - defining objects and conditions, restricting player actions, determining effects on players.  

Note that games and players often fall in to one of two camps. The first camp says you can only do things the rules explicitly say you can do and the second camp says you can do anything the rules don't explicitly say you can't do. The two camps seldom play well together.  

## Resources

These are game objects that have a value for players in reaching their individual objectives. The value of these items can be determined by their **scarcity** and **utility**. The value for players (i.e., utility) is often scaled by how much an item helps a player achieve a goal.

Common resource examples in games - Lives, Units, Health, Currency, Actions, Inventory, Time.

## Conflict

Conflict emerges through procedures and rules in the game that prevent a player from achieving their goal. Objectives often guide players to these conflict situations.  

Common conflict types include -  
* **Obstacles**. These can be in physical or mental form. Physical obstacles could be the length of your Pinball flippers or the bumpers that the ball bounces off of. Mental obstacles can be a missing item to complete a riddle in an adventure game or the challenge of calculating the right numbers in Sudoku.
* **Opponents**. Other players in a game or computer-controlled enemies.
* **Dilemmas**. These are problematic choices that a player is faced with. It’s a strategic decision, where the consequences have to be weighted before proceeding.

## Sequencing

Sequencing is the order of play, what happens when. There are many possibilities.
* Pure turn based – one player at a time in order
* Turn based with simultaneous resolution
* Turn based with interrupts
* Turn order varies by round
* Real time
* Player in last place plays next

## Game Atoms

We can define the smallest possible design element as a game atom.

* **Players/Avatars/Game bits**. Players set the rules of the game in motion and often have some form of representation in the game world (e.g., tokens or pawns). Some games don’t have representations and the player represents themselves.
* **Objectives/Goals.** Often referred to as missions or quests, they are like a task list for your player telling them what they should be working toward.
* **Rules/Mechanics**. In games, mechanics determine how something works, much like game rules do. They are about the possibilities for the players that will change the game state. Rules are the most defining quality of games. The following are general properties of rules: limit player actions, explicit and unambiguous, shared by all players, fixed, binding, repeatable.  
* **Resources**. See above.
* **Game States.** The state of the game system at one point in your game loop. Essentially everything that you would write into a save file. A collection of all relevant variable game information that changes during gameplay.
* **Game Views**. Different stages of the game may allow a player to see different information. The parts of the game state that are visible to a player are called the game view.
* **Information**. All the information necessary to play the game.
* **Sequencing**. The order in which rules unfold, similar to turns in a board game. This is important for thinking about when the information in a game changes (and with it the current game state).
* **Player Interaction**. The types of interaction allowed for players.
* **Theme/Setting**. While a setting is not mandatory for games, many games have some sort of theme that helps players to make sense of game information. It is what the game is all about. This can refer to things such as colour, theme, story or narrative. It helps players feel more at home with your game mechanics.



