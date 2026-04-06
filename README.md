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
