# SWARMMO

A new type of free-to-play browser MMO! Featuring high player counts, dynamic AI enemies, and fast-paced combat. 

Battle large groups of enemies with your fellow players and work together to push-back the orc hordes who roam the world seeking to gain new territory and expand their numbers. 






**Playtest**: ~~March 2024~~ April 2024

**Release date**: ~~April 2024~~ May 2024

** UPDATE ** : The release schedule has been delayed by 1 month! Hopefully its the only delay but who knows...
Things are very close. I'm dealing with some challenging problems related to directed graphs, relational algebra, and topology. The final frontier~
Once this part is done, the game will be ready to test and I can also start focusing on adding content. Soon (tm)

** UPDATE 2 **: I'm in the final stretch! The hard problems are now solved :). Now whats left is to update the UI and add some additional client-side functionality. Also I need to debug some client-side animation issues. I really want to work with a 2D artist so I can start adding more content and give the game a more consistent art style. Small steps.
Last month motivation was low. But I'm entering this month with much higher motivation. Gotta show up everyday and put in some work, only way to get through a slump. 

**UPDATE 3** SO so so close. But you know - the last 20% is like 80% of the work. haha. I'm picking and choosing where to spend the time. Some of this will get refined in the playtest so no use chasing perfection. Right now I'm back to making some adjustments to the AI logic - the AI wander algorithm needs to be tweaked to look more "realistic" because right now its just too erratic with the AI making too many turns and not taking breaks to enjoy the view. But the AI is very good at chasing players down once they are in line of sight so thats good! As for the game UI, its mostly done. I'm going for a minimalist UI anyways, and the UI will be expanded as more features like custom equipment, inventory, etc are available in the future. 

Also the map has been expanded by 2x  and feels quite big now. I don't know what the play-test player limit will be - 100 players? Theoretically 1000+ players can be supported but that will make the map too crowded and also I don't want to get hit by some crazy cloud bill *if* somehow I do get that many players - doubt it.  

AND I implemented mandatory client time synchronization! It works really well. Whenever a player spawns into the world - they are invunerable for a period of 10 seconds and must exchange SYN packets with the server untill the server determines sufficient sync. Untill then, no other input is accepted by the server. This period is also used to calculate the average latency on the client-side using sampling and the midpoint method. I can also have it so the server can boot the client if the latency is too high or if the sync is not sufficient after 10 seconds. 

Oh yeah also I quit smoking ciggarettes a month ago! So I'm 1-month smoke free. But I'll probably start again some time in June~ or maybe when I'm cash flow positive again. 

Regions:

- NA WEST
- NA EAST
- EU WEST


Unsupported browsers:
- Safari





![image_1](https://github.com/mikhmha/SWARMMO/assets/75456828/de69cda4-665a-4762-85eb-77221634d586)

