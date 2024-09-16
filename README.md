# SWARMMO

A new type of free-to-play browser MMO! Featuring high player counts, dynamic AI enemies, fast-pased combat, and a beautiful modern 2D isometric art style!

Battle large groups of enemies with your fellow players and work together to push-back the goblin clans who roam the world seeking to gain new territory and expand their numbers. 
Make your character stronger by completing quests to gain loot and experience. 



**Playtest**:  **VERY SOON**

**TRAILER**: Its being made...

Game is so close. Now im implementing the matchmaking system. You take the game world and partition it by some arbitrary division criteria and represent it in code as some data structure contained in a list or kv map. Then you iterate through all of them at some INTERVAL and use some heuristic you figure out based on gameplay to select the best one to spawn incomiing players or ai units into. Its innovative? I don't know all the details yet. IT will come to me in a dream. But it feels like im procrastinating because I really want to launch before October. And NOTHING is coming to me. The implementation is done but I don't know what heuristics to use or what INTERVAL will be the best most fun for players. Part of it involves maximising the rate at which players spawn so you always have people shuffling through = and the assumption is that a very small amount of players will play beyond 1 session, most pop in and out. they are transient participants. and the world meets incoming spawn demand via spawning in some corresponding amount of AI enemies. blah blah. its cool, fun, bandwidth efficient. 

![zone_concept](https://github.com/user-attachments/assets/dcad0a02-3a34-4829-a2e7-5c89593cd123)
ALSO THE WORLD DESIGN will end up changing heavily and better reflective of the partitioning scheme. There is a visual element to it. But will the level design changes happen before launch, after launch, etc? The problem is I LOVE making the map its so fun. Its like painting. But thats the problem. ITS TOO FUN. Hours pass by. And then nothing on the coding side gets done. So I live with whatever the hell the map is right now.  I WANT MORE TREES AND GRASS. There are "primary zones" 0-3 and "transitive zones" A-F. What is the disctinction, does it mean anything? I DONT KNOW YET but i know its legit. And sometimes you can cross between zones and sometimes you can't. But I don't know when. 


 [SEPT 12, 2024] 

OMFG I've been procrastinating. Because this world spawn matching problem is so interesting and will make the game so fun and complete. I tend to procrastinate every few weeks (6-8?) for a week and then it passes. So this should pass too. I don't know if I start to write because things are good or if things are bad. IS it all a form of cope?  Maybe the summer ending is filling me with dread. Because I was so looking forward to it a few months ago but in the end it was just OK and last summer was way better. This summer I mostly worked on the game. Its not a bad thing, I had fun on the things I worked on. But also when I look back I go - wtf did I work on? Because every 2 weeks you go from "MY GAME IS AWESOME" to "MY GAME SUCKS NO ONE WILL PLAY IT" and its an eternal cycle. Last summer was fun because I was so care-free and spent a lot more time outdoors. This summer I've been working on the game and its like an all-day thing, not a clock out after 5pm thing. And then there is a great contradiction, because I was more care-free last summer but also way more miserable and unfullfilled internally. no regrets. In a few days we will be back on that MY GAME IS AWESOME grindset. and everything will wash away.

**[SEPT 15, 2024]** 

OK I GOT IT. I know how to solve the spawn matching problem. Up untill now my idea of it was a "match-making" system that was spawning enemies in response to player demand. The player demand being an incoming wave of players waiting to spawn. I couldn't understand how to properly model this. How can the AI Director effectively respond to transient conditions? It doesn't know how many players in an incoming spawn wave are going to stay vs leave. I was doing things the wrong way! What I actually should be doing is implement a system that responds to AI demand! Players are spawned in relation to what decisions the AI director makes, not the other way around. This also avoids issues with too many enemies or too many players being spawned in the world at once. Because if the world is at max capacity, then you can simply just turn away new connections and tell them "Try again later". And the capacity can be based on some dynamic conditions.  And of course the conditions are such that the house always wins. 

There may be scenerios where players aren't spawning into the world for some time, maybe things in the world are super hot. The director knows its chances are low so it tells the match-maker "STOP SPAWNING NEW PEOPLE IN IM GETTING OWNED". Well these sorts of scenerios should be avoided because we dont want people to be waiting too long to play, that SUCKS. So the gameplay balance will focus around that. You shouldn't be waiting more than 30 seconds to spawn in. IDK don't quote me on that, its not a hard target. 


the AI director system is so interesting now.  its an independant process that runs alongside the world simulation and receives asynchronouse updates which it uses to update its decision making. 
the decisions it makes will fall into the following: 1. Spawn in a new squad, 2: Redirect an existing squad, 3: A mix of both. 
our AI is A* decision making all the way down. thats crazy. From spawning, to the individual unit action level. 


**[Sept 16, 2024]**

Yeah i always look back and realize i wrote some word vomit. Well atleast you know its not some ChatGPT generated writing. Ok after yesterday I really understood what I'm trying to do, then I crossed notes by reading into how Valve implemented the AI director system in Left 4 Dead. I actually never liked or played those games that much but i always found the director system interesting. I haven't played the games enough to really understand how the director  affects gameplay across all the maps and difficulty levels and game modes, etc. But thats not really the point. The publically available Valve technical slides on AI director implementation explain the underlying problem domain and how to represent it in perfect detail. Summary: Techniques to implement Procedurally Populated Environments. OK i'm done procrasting. So I won't write again for a while. No need!



![Image-203](https://github.com/user-attachments/assets/fcbaf0f7-1f41-4417-9237-0d75fe54ae62)

![game_2](https://github.com/user-attachments/assets/865de44a-33bc-4a46-b0c8-adee222db2ec)

![game_1](https://github.com/user-attachments/assets/1da3106d-30a3-4a10-9d34-707034950709)

![game_3](https://github.com/user-attachments/assets/be1eed0f-d497-46a3-a7dd-7eaef591ae68)
![game_inventory](https://github.com/user-attachments/assets/07ebf85b-6d7d-4883-8dcb-a65cad2377e2)

Regions:

- NA 
- EU



Unsupported platforms:
- Mobile / iOS, Android

Unsupported browsers:
- Safari
