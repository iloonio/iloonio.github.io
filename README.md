# Silt's (Ruslan's) dev blog for DH2650

This page is going to document my own contributions for the game design course at KTH with the course code DH2650 (make a ink here).

---

## 2026-03-25 - First meeting

I booked the group's first meeting, where we spent a lot of time talking about our interests, what games we've played, and such. It took some time, but eventually all of the group members began opening up about their experiences :) This lead to a wonderful brainstorming session where we finally came up with our game idea! We used Figma to brainstorm, which included writing down all kinds of ideas until we found something that we really wanted to refine. It makes me really glad that I'm in this project with two interaction design students, since they're very familiar with brainstorming and the creative process.

## 2026-03-30 - Personal Reflections

I think the hardest part of game development in groups is _alignment_, for lack of a less corporate-sounding word. Each member has their own idea for how this game will look and feel, even though we use the same language to describe it. The most important part right now is to bridge our respective gaps and work towards a shared mythos of what our game is supposed to be.

It's kinda nice that we use Figjam for so much of this. It lets us share ideas and structure them in a non-linear fashion. I've written down my own ideas for the game, and it seems like my team has done the same! I am excited to meet today and finally start working on some tangible stuff.

### Making a Multiplayer Game

After doing a short research session about making a multiplayer game, I have come to the conclusion that it would be best to make a client-hosted Unity game. Godot's multiplayer solutions just cannot hold up to Unity as of now, as much as I would love to work in Godot. There's some thing called Relay I think? We can host our game through that I think. I will have to do some more research into that.

### Dump from personal notes
Give more depth to the potion system:
- The cauldron has a simple “cook” mechanic. Ingredients inside are cooked. Then, by holding a bottle and interacting with the cauldron again, you fill the bottle with an elixir. 
- Some Ingredients need different amounts of cooking time for their effect to materialize. If certain ingredients are overcooked, it might result in a terrible reaction. 
	- Example #1: Gunpowder only needs to be cooked once to have an effect. However, if gunpowder is cooked together with cinders, it will cause the cauldron to explode.
	- Example #2: Red cap mushrooms need to be cooked thrice in transmit its enlarging effect. Otherwise it acts as a poison that puts you to sleep. 
- Rename gunpowder to Sulfur. 
- **Reason for adding this:** It gives potion crafting more depth, and creates unpredictability, which I feel is at the core of wizardry.


#### Game design pillars
Ranked from Most Important to Least Important, but all are vital. 
##### Crafting 
- Alchemy is all about making a concoctions to solve problems! Crafting should be integral to the gameplay loop. 
##### Chaotic 
- Alchemy and Wizardry is often unpredictable, and this should be reflected in our potion crafting & environment design. Let actions have consequences that teach the players what to do & not do. 
##### Social
- Players work towards a common goal and their decisions should impact each other, whether they are working towards that common goal or not. 

## 2026-03-31

We had a hybrid meeting where we discussed some question marks regarding game design. I setup a Github Repo with a Gtihub Projects attached to it. I also put up some issues on our KanBan board, I'm hoping people will use it! 

I told the group that I'd be down to do the elevator pitch & presentation essentially solo, Lugina has helped out a tonne with the business case however, so thats nice :) Aside from that, Yufan has made plenty of sketches that I can use in the presentation, so I have some good material to show during the presentation 

## 2026-04-01

Happy April Fools!

I've more or less finished making the slides for the presentation tomorrow. I feel like freestyling it a little. It sucks that we haven't started writing anything in the GDD yet, I wish our lead Game Designer would've written down the base mechanics at least. Currently it's still all up in the air so i suppose whatever I present tomorrow is what I *think* the group thinks we are making. Either way, I think it will be fruitful.

I want to start coding on this project so I can learn how multiplayer game development works. I want to ask if there are any good resources for it so I can save time on researching. 

## 2026-04-04 - 2026-04-06

Ok so quick recap for these past three days! I've managed to make multiplayer for in Unity, I just need to test if my solution works remotely. With that said, I think I have a firm grasp of Netcode for GameObjects now, so I should be able to easily convert anything my team makes into viable multiplayer code.

Aside from that, on April 6th, we held a group meeting where we wrote down the concrete goals for our Prototype, I then divvied up the work. I also finally began editing the GDD, being the first and so far only person to start writing stuff down in it hahah. It's not a big deal though, since we use our Figma as the living document, while the GDD is just the formalized version of it.

## 2026-04-13

I haven't been writing much in this blog, because i've been doing lots of work on the project. Namely, I have been devising how to do random map generation, and with Björn's dissuation, I've decided it to be outside of the scope of the project. Here it is anyway: 

### Random Generation
![initial](image-48.png)
Suppose we have a NxN grid that represents the game world. The Cauldron will spawn at a set location on this game world, and the cauldron room will always have three doorways leading to it. 

![random1](image-49.png)
Now, Randomly Assign Four Gardens on the grid, these are not allowed to be directly next to the Cauldron.


![Paths](image-50.png)
Then, do a [[DFS properties|DFS]] search with a randomly chosen direction from each garden towards the Cauldron as the end location. The only limitation is that the DFS is not allowed to go to a Garden Node. DFS is allowed to visit nodes that have already been visited, but it is not allowed to go through a connection that has already been walked through. 

![Ingredients](image-51.png)
Then, Assign each Garden an Ingredient and assign a Shortcut Path at a few randomly chosen and unassigned Paths, and also at one previously assigned path (but never directly to a garden). Shortcuts are paths that can be unlocked by either setting an obstacle on fire and/or blowing it up
![](image-52.png)

And now randomly assign different room prefabs to the unclaimed tiles! There are some rules to this however: 
- First, each room is assigned two values: **Difficulty** and **Number of Exits (NoE)**. 
	- Difficulty basically means how hard the room is to pass through. It’s a heuristic for map creation, ranging from integers 0 through 2. Room prefabs will have a Difficulty rating attached to them, which the generator uses to assign prefab rooms. Difficulty is assigned with Perlin noise, where values assign the following difficulty: 
		- $mat(0,0.4)$ : 0
			- 0: Players can pass through without any tools to help whatsoever, even if miasma would occupy half of the room. 
		- $mat(0.4, 0.8)$ : 1
			- 1: Players don’t need tools to pass through, assuming no Miasma occupies the room.
		- $mat(0.8, 1)$ : 2
			- 2: Players will need tools to pass through, assuming no miasma is present
- Second, we go through each tile and assign it a room based on Difficulty and NoE, with NoE taking priority over Difficulty. If a a specific Difficulty-NoE configuration exists, it will pick the next possible room with matching NoE and closest match Difficulty. 
- Thirdly, in paths where we have marked shortcuts, we put an obstacle in the way. Obstacles can come in three flavors and are chosen at random: 
	- Flammable Obstacle: Ignite it to clear it. 
	- Breakable Obstacle: Explode it to clear it.
	- Vertical Obstacle: A high wall blocks the path. Find some way to scale it.

That’s it! You now have a fully-generated game map. It will require the following minimum prefabs however:
- Atleast one room prefab for every NoE configuration.
	- 1 NoE: 1 room prefab $times$ 4 rotations. 
	- 2 NoE: 2 room prefabs $times$ 2 rotations.
	- 3 NoE: 1 room prefab $times$ 2 rotations. 
	- 4 NoE: 1 room prefab

I am starting to think that it might be better if we have separate prefabs for walls with their NoE, and a set of prefabs for the difficulty.

## 2026-04-14
I sat for 4 hours trying to code multiplayer. It should've taken me at most 2 hours, but the last two hours were spent trying to integrate existing code into multiplayer. I am going to bring it up with the group and ask the coders to at the very least keep all of the logic for player interaction inside of the player interaction script (Why is it spread out across two files anyway?)

At the very least, I made a functional lobby that connects to unity sessions and loads players into the game world. Player movement is synced, but object interaction has to be patched up. I am gonna bring it up on the meeting tomorrow.

## 2026-04-15
Today we have a meeting where i will bring up my woes... Perhaps I am in the wrong here? We'll see 

I haven’t written in this blog for a while, and that’s because I’ve had a lot going on! So i will try to condense my contributions to what I’ve managed to do *every week* instead. 

## The big Recap

### April 19th → April 25
I am pretty sure I taught Lugina how to use Blender & Unity this day. Not sure though. Anyway, that took a lot of my time. To me its felt like the thing I’ve primarily done during this group project is manage the group rather than put down work itself. I remember being very antsy to start working on the game at this point. 

### April 26th → May 2nd
I coded multiplayer, i spent so much time learning how unity works until I got a functional prototype of the multiplayer. Aside from that, I’ve mostly just been leading the group, which has been a bit exhaustive but its been so much fun! Working with people from multiple disciplines is a very gratifying job for me. 

Looking through my daily notes, it seems like I spent a lot of time trying to comprehend Shuangyu’s alchemy code, at the same time as I was trying to adapt it to Unity Netcode. I learned all about network variables, network propagation, spawning vs instantiating, how despawning should work, etc. It took a lot of time, but eventually I got it all working. 

The final solution for the week was a botched server-client architecture with some elements of distributed authority archiecture. In practice this meant that the server & client would both be responsible for the game state, with physics and all, with clients gaining authority of objects that they pick up & touch. 

Also i had severe wisdom tooth pain this week, so working was generally difficult. 

### May 3rd → May 9th
I booked a really long meeting where we’d work on different parts of the game together in the same room. I divvied up the work, so everyone knew what they were going to be doing, and I gave this in bite-sized pieces. Most of the time, I wasn’t even coding. I was mostly just answering questions, communicating across the two sub-teams in our team, it was really intense but so invigorating.

Barney decided that the code base needed some cleaning up in order to scale, I agreed and let them know that I think its a good idea. To my surprise, they had indeed restructured literally the entire repository, and it was so amazing. The new code base felt so much easier to work with it. That being said, they had to rewrite almost all of the old alchemy code in order to make this change, so that work was sadly lost. Although, to be honest with you, I prefer the new code much more. It doesn’t have a rancid code smell to it, and I catch far less AI-abuse whiffs from it. 

The new code base was flawed however. A lot of things didn’t work as expected. So, we decided that for next week, we would comb through it and fix every bug. 

### May 10th → May 17th
Me and Barney sat from 13:00 to 21:00 coding multiplayer in the refactored code base until it worked. We initially planned on doing some level design together with the Designers of the group, but Barney did not do the extensive testing that multiplayer required (Unity netcode often fails silently, so you have to thoroughly test everything at run-time). 

Along the way, we discovered that the old code base suffered bugs that weren’t initially apparent (I hadn’t done thorough enough testing on the code base either, apparently), but became so once we started comparing the old with the new while investigating how we’d implement multiplayer for the new code base. It felt cathartic to have someone else to speak with about coding multiplayer, especially since I was already so familiar with unity netcode and its many quirks. Using AI was completely pointless, not that we even tried to. We mostly coded by ourselves, trying to turn Unity’s vague documentation and the old “solve-by-intuition” code from the multiplayer code base that I wrote. I am very happy to be working with someone like Barney: Someone who has more coding experience than me, who can teach me the best practices, while I handle the group communication, code legibility, and knowledge transferal.

Once everything was finally ready, we could actually start working on the game with the new code base. I synced the designers, booking a meeting with them on Tuesday where I helped them get the latest version of the game running, while also making them feel more secure in using Git & Github. I also taught them some small tips & tricks about Unity which I picked up while sitting with it for a long time. I also taught them the basics of the changes we made to the code base, such that they could start building the level in Unity. 
In return, Yufan offered me amazing chinese green tea, and Lugina gave me a donut :-) a fair trade.

On Wednesday, I merged everyone’s branches, there were some issues however that took time to sort out. Shuangyu started touching code that wasn’t part of his delegation of work, this is likely due to him misunderstanding that when I delegated out the workloads, I expected them to *only* touch their own tasks and not bleed out into doing other people’s work. This caused some tedious merge conflicts which took me some time to correct, culminating with me telling him exactly what behavior the code should produce, and what he should have changed. Once that was done, I looked through the changes Barney & the Designers made, and then I modified the cauldron to behave more like what we wanted it to be (it had a mesh collider to start with)

After that was sorted, we had our first real playtest! IT was a bit janky at first, but we did eventually get it to work and it was really fun to see our work be present & existing.
