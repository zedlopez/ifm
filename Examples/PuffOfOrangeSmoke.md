Example: ** Puff of Orange Smoke
Location: Action variables
RecipeLocation: Combat and Death
Index: Redirecting all actions from one object to another
Description: A system in which every character has a body, which is left behind when the person dies; attempts to do something to the body are redirected to the person while the person is alive.
For: Z-Machine

  
Suppose we want to let the player kill characters, leaving behind corpses.

  

``` inform7
{*}"Puff of Orange Smoke"

Paraguay is a room. Bolivia is north of Paraguay. Lydia is a woman in Paraguay. "Lydia is, as usual, here." The description of Lydia is "Long, long legs and a sarcastic attitude." Instead of touching Lydia: say "'Watch it, sailor,' she snaps."

A body is a kind of thing. A body is a part of every person. Instead of touching a body: say "[The noun] is grotesquely inert."

The description of Lydia's body is "Long, long legs and no attitude at all." The initial appearance of Lydia's body is "Lydia's corpse is sprawled at your feet."
```

  
Using our "part of every person..." line, we've conveniently assigned one body per person. Since we're going to separate people from their bodies when the bodies die, though, we also want a more permanent relation that will help us keep track of which bodies used to belong to which people:

  

``` inform7
{**}Spirit-possession relates one person to one body. The verb to be owner of means the spirit-possession relation.

When play begins:
	repeat with victim running through people:
		let the corpse be a random body which is part of the victim;
		now the victim is owner of the corpse.
```

  
When Lydia is alive, we want >``touch lydia``'S ``body`` to mean the same thing as >``touch lydia``, so we use the setting action variables rules as a convenient point at which to reassign the action:

  

``` inform7
{**}Setting action variables when the noun is a body which is part of a person (called owner):
	now the noun is the owner.

Setting action variables when the second noun is a body which is part of a person (called owner):
	now the second noun is the owner.
```

  
This doesn't change Inform's idea about what action is being performed; just about the object it's being performed on. The rest of the action will now proceed as if the player had typed >``touch lydia``.

  
Along similar lines, once Lydia is dead, we want >``move lydia`` to mean >``move lydia``'S ``body`` if the body is in view:

  

``` inform7
{**}Setting action variables when the noun is a dead person and the noun is owner of a visible body (called the mortal remains):
	now the noun is the mortal remains.
```

  
The trick is, though, that >``move lydia`` will only be understood if there is something called Lydia that the player can see and refer to, even after she's dead. There are various ways to do this, but the least painful here will be to make the deceased Lydia permanently visible, by putting her in an always-accessible backdrop. The backdrop itself will never be mentioned in the game, and we should make its name something that the player is unlikely to type casually; we don't want the player to interact with it directly. So:

  

``` inform7
{**}The worldview is a privately-named backdrop. It is everywhere. The spirit-world is a privately-named transparent closed unopenable container. It is part of the worldview.

Definition: a person is dead if they are in the spirit-world.
```

  
It's also possible that the player will type something like >X ``lydia`` when Lydia's corpse is not in view, so we should have an appropriate answer to that as well:

  

``` inform7
{**}Before doing something to a dead person:
	say "[The noun] is dead; or had you blocked that out?" instead.
```

  
Because the before rules happen after the setting action variables rules, this will only ever happen if the corpse is not visible.

  
Now we define the attack itself, which should discard the body, move the spirit to its eternal resting place, and describe the event to the player:

  

``` inform7
{**}Instead of attacking someone:
	let the corpse be a random body which is part of the noun;
	move the corpse to the location;
	move the noun to the spirit-world;
	say "With a single blow, you rid the world of [the noun]."
```

  
And finally a trick borrowed from the chapter on understanding, so that we can refer to "Lydia's body" while Lydia is alive, but "Lydia's corpse" only after Lydia has died:

  

``` inform7
{**}Understand "corpse" as a body when the item described is not part of a person.

Test me with "x body / x lydia's body / touch lydia's body / x corpse / kill lydia / look / x lydia's body / x lydia's corpse / x corpse / x lydia / touch lydia / lydia, hello / n / x lydia / touch lydia / lydia, hello".
```

