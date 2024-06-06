# SWARMMO

A new type of free-to-play browser MMO! Featuring high player counts, dynamic AI enemies, and fast-paced combat. 

Battle large groups of enemies with your fellow players and work together to push-back the orc hordes who roam the world seeking to gain new territory and expand their numbers. 






**Playtest**:  **June 2024** ~~April 2024~~ ~~March 2024~~ 

**Release date**: **June/July 2024** ~~May 2024~~ ~~April 2024~~ 

** UPDATE ** : The release schedule has been delayed by 1 month! Hopefully its the only delay but who knows...
Things are very close. I'm dealing with some challenging problems related to directed graphs, relational algebra, and topology. The final frontier~
Once this part is done, the game will be ready to test and I can also start focusing on adding content. Soon (tm)

** UPDATE 2 **: I'm in the final stretch! The hard problems are now solved :). Now whats left is to update the UI and add some additional client-side functionality. Also I need to debug some client-side animation issues. I really want to work with a 2D artist so I can start adding more content and give the game a more consistent art style. Small steps.
Last month motivation was low. But I'm entering this month with much higher motivation. Gotta show up everyday and put in some work, only way to get through a slump. 

**UPDATE 3** SO so so close. But you know - the last 20% is like 80% of the work. haha. I'm picking and choosing where to spend the time. Some of this will get refined in the playtest so no use chasing perfection. Right now I'm back to making some adjustments to the AI logic - the AI wander algorithm needs to be tweaked to look more "realistic" because right now its just too erratic with the AI making too many turns and not taking breaks to enjoy the view. But the AI is very good at chasing players down once they are in line of sight so thats good! As for the game UI, its mostly done. I'm going for a minimalist UI anyways, and the UI will be expanded as more features like custom equipment, inventory, etc are available in the future. Also the map has been expanded by 2x  and feels quite big now. I don't know what the play-test player limit will be - 100 players? Theoretically 1000+ players can be supported but that will make the map too crowded and also I don't want to get hit by some crazy cloud bill *if* somehow I do get that many players - doubt it.  
AND I implemented mandatory client time synchronization! It works really well. Whenever a player spawns into the world - they are invunerable for a period of 10 seconds and must exchange SYN packets with the server untill the server determines sufficient sync. Untill then, no other input is accepted by the server. This period is also used to calculate the average latency on the client-side using sampling and the midpoint method. I can also have it so the server can boot the client if the latency is too high or if the sync is not sufficient after 10 seconds. 
Oh yeah also I quit smoking ciggarettes a month ago! So I'm 1-month smoke free. But I'll probably start again some time in June~ or maybe when I'm cash flow positive again. 



**UPDATE 4** Made some really good breakthroughs this week. The AI is working amazingly! Understanding how the a.i works with the server has come in waves. But now I can conceptualize it all very well and it makes a ton of sense to me. I like making diagrams but only after the fact. So here is a diagram of my AI architecture. Its taken a while to finalize this and lots of debugging + performance profiling + experimentation. But it was worth it. The AI can be very extensive in the future - even control groups can create units with variants and different stats. Very exciting stuff. I don't know if people have tried this stuff in Elixir. But its not all good news. Unfortunately I started smoking again. I was doing so good. hahaha

![Capture](https://github.com/mikhmha/SWARMMO/assets/75456828/cd6ea3bc-9fa1-490d-97c2-f2ed5e62500a)


**UPDATE 5** OK things are going really good right now. I've updated the release date targets - and I really, really, really think this will be the final delay. Recently I've been plowing through the remaining work - I get a lot of output for very little input (code written) which is also very motivating. it the cigarettes? Am I just a dopamine chasing hamster? Why do i require things like rituals and bad habits to feel motivated? I don't accept any pathological answers for this question. Everyone says they have ADHD these days....

I think the more rational reason for the increased work output is because enough systems are in place now for me to execute? Lots of the work in March and April was design/planning heavy and required lots of thought on paper and then subsequently testing with mock inputs and verifying outputs. Lots of days were "thinking days" where not much code was written and I spent more time doing other stuff while waiting for background processing jobs in my brain to finish and reveal the answer - __it came to me in a dream__. So it didn't feel like I was progressing. And each time I booted up the client-side to test I'd feel some dread because the game played and felt like shit. 

But now..its very interesting. These past few days I find myself actually playing the game. Seeing how the AI reacts to the player is quite fun and exciting. Initially my goal with this game was to be more of a Proof-of-Concept thing - I wasn't expecting it to be very engaging at all - I figured that type of stuff would come months later, after I got some more art assets and (possibly) funding.   

So here is the remaining work left before I do the playtest. 

1. **Notifications System** [COMPLETED]
After a client connects to the server - they receive 2 types of updates. World State Updates (used for rendering) and **notifications**. Notifications are client-specific messages used to update the HUD and NOT subject to interest management - whereas world state updates are. The notifications system is already in place - but what I need to do is add more notifications for certain events (spawn, stat changes, event join, event complete) AND implement message batching for notifications. Because most notifications are small in terms of data and it doesn't make sense to send each as an individual packet every tick.  Also these notification updates will tie in with the remaining UI work needed on the client-side. 

UPDATE: OK I finished the work on this. It was good to finally tackle this. Finishing it allows me to debug server events much easier on the client-side now. And in godot i implemented a very straight forward ui "card" element that is displayed on the player hud. this sort of UI work is so easy in godot. Events with multiple participants and turns have their notifications delta encoded - world entity id's are encoded as relative indexes so a notification encoding an interaction between 2 entities goes from minimuim 8 bytes to 2 bytes. All notifications generated for a client during a tick process are batched and sent as one packet to the client. The batched notifications are in the order of "processing" insertion, and its up to the client on what to do with the notification - render it as a ui element on hud, display some text, etc. 

~!2. **Finite-Domain Constraint Solver for AI Unit Generation**~ (SEE UPDATE 6)
I got around to reading this paper on how to roll your own Finite-Domain Constraint Solver. Very interesting stuff. This will be used in the AI Subsystem to generate/spawn AI control groups with random attributes that conform to the constraints specified. So it will make things very interesting gameplay wise. The constraints will be things like unit stat allocations, unit graphic variations, unit "role" variations (X leaders and Y followers), etc. I'm not going to go overboard with the constraints initially, I think even keeping things simple will yield lots of interesting results. 

~3. **AI Unit Steering Behaviours**~ (SEE UPDATE 6)
This is already in place, but I want to spend some time experimenting with the different steering behaviours - specifically Queueing behaviour and Leader Following. 

~4. **Game Client Shaders + Level Tweaks**~ (SEE UPDATE 6)
Well I want to have some fun with shaders on the client-side. I think I can do some cool stuff that will let me create AI distinct unit variations without having to do asset work. Also maybe some environment shaders for the grass and certain tiles. And also since we have world-serlization in place now (for the server) I can add more obstructions into the game world and they will have server side collision! So more fences and walls and that type of stuff. Maybe even cliffs? 

~5. **World Server Connection Queue**~  (SEE UPDATE 6)
This is all remaining work before deployment. Implementing some queue system to restrict the maximum allowed players because the map isn't big enough and I don't want to get hit with some expensive cloud bill. And this work will also tie in with the whole connection-auth-process. So its like the LAST (for real) thing before playtest. 

When I write it down it seems like theres a lot left. SO maybe I'm underestimating the work left. But also I already know how I'm going to go about implementing all of the above into the existing systems. So not much "thinking" more coding and wrapping existing abstractions. OK I go back to work now. wish me luck. 


**UPDATE 6**: 

OK - my previous update the remaining work listed there is now out of date! Because 2,3,4,5 are being tackled simultaneously right now. Its good to know when existing goals can be revised! Because the thing with this type of work is that the systens you've spent time building and testing are now giving you back BIG returns. Its a temporary force multiplier and you remember why you built them in the first place. So now the wave has come and you have to ride it. If you can get a lot of mileage out of these temporary boosts then it means you built (and designed) a good system. 

BTW - I feel really confident in Godot now. I have a good handle on it and I know how it works under the hood.  I don't have to look up much things at all at this point and I don't have any superstitions in my workflows. When to use a scene, when to make scripts (write code), how to test with or without writing code, when to use signals, what plugins to use, how plugins work, when to preload and instantiate children, what is a scene, what are children? I know it all. And before i started this project i knew nothing. Godot is the shit. Its the best thing ever. If Godot has 0 fans, I'm dead 😫❌




I got a dilemma now actually. Because I can start posting some screenshots and videos cuz now im satisfied AND the game looks QUITE different now in a very good way (it looks LEGIT). So should I continue from here by using a psdueonym and posting on relevant online nerd spaces? Because if I catch attention then I don't want to be linked to my real id. 

BUT its a gamble. Because its all up to chance if your game gets attention (though not completely). And you might get a lot of interest for a day or whatever and then things fizzle out. SO you want to time when you post that sort of stuff. Ideally when you have something to actually try. Sometimes you "blow your load" (crude) too early by getting 1k upvotes for a screenshot from your dev build on some game subreddit. And then release time no one really cares. EH can't blame them - I've done this same thing exactly. If you have something to try then atleast players can try it and tell you if it sucks. If it sucks ATLEAST you tried it. I won you consumed my product. So the jokes on you. 

A certain guarantee (nothing is guaranteed) is IF:  when the game is ready to play (2 more weeks^2 more weeks) I post it on HN as a Show HN post at the right hours than I could get some buzz. Usually show hn posts that are interactive get 50 votes (all i'd want). The internet has lots of lurkers. I'm also confident because my HN account is in good standing - idk if the site actually does it but I also bet it does - because its like 90% affected by your account creation date. Otherwise your posts get downranked and weighed more heavily as spam. So I don't want to do it from a new "throwaway" HN account. 

HOWEVER, posting from my HN account gets me doxed. BUT its a good thing because the people that doxx you from that site are cool and can offer you jobs! So I do want to be doxxed from HN - no issues there. BUT then what IF the game gets a lot of buzz from players (i want that more than a job tbh) well now you can get doxxed by them via your HN post. I want players... I don't want players! No I want players for sure - thats way more motivating. 


So you see my dilemma? All these BUTS and IFS are no good.  

**UPDATE 7**

I'm at peak motivation right now. Things are going VERY well. The game looks and plays COMPLETELY different now. All the screenshots posted to date are VOID at this point. It will be fun to look back at them and see how everything evolved. I'm close to dropping a gameplay snippet - just a bit more work on my end. Ahh I'm so excited. Because I didn't imagine the game would look or play how it does at the current stage . And overall this project has gone so smoothly - I make goals on a week-by-week basis - I reach those goals or wrap the goals into bigger milestones and I move forward week by week. I haven't had to fight any of the tools I'm using or spend days debugging some issue with them. Everything I use fits in to my workflow. And I have workflows for the backend, front-end, asset creation, animation testing, map creation, etc you name it.

Also, I'm once again 1 month smoke-free! Haven't had or craved a cigarette since then. And I have to be honest with myself - my work output has remained the same and/or increased. So we can objectively say cigarettes do not make me productive, its all an illusion. But what DOES make me productive? Vibes? The sun? Maybe the answer is to just not analyze this because its too easy to convince yourself that some secret thing makes you more productive. another false illusion. hmmm. thats why i don't read or watch that self-help crap about how to be more productive. Smoking was fun in the winter though. Nothing like standing outside in the cold air and chainsmoking while thinking about some system architecture bullshit. 

Regions:

- NA WEST
- NA EAST
- EU WEST


Unsupported browsers:
- Safari





![image_1](https://github.com/mikhmha/SWARMMO/assets/75456828/de69cda4-665a-4762-85eb-77221634d586)

![game_2](https://github.com/mikhmha/SWARMMO/assets/75456828/dafca50b-538e-4e43-971b-48d3ac1ce8d8)
