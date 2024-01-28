Example: **** Sand
Location: Before rules
RecipeLocation: Taking, Dropping, Inserting and Putting
Index: PUT and INSERT automatically TAKE first even with multiples
Description: Extend ``put`` and ``insert`` handling to cases where multiple objects are intended at once.
For: Z-Machine

[ZL: https://inform7.atlassian.net/browse/I7-2348 ]::
  
The above example does not quite work when we want the player to be allowed to take multiple objects at once before putting them somewhere: we also need to add a couple of "understand" rules borrowed from many chapters later. While the reasons may not be immediately clear, we include the demonstration here for the sake of thoroughness:

  

``` inform7
{*}"Sand"

Before inserting something which is not carried by the player into something:
	if the noun is in the second noun, say "Already done." instead;
	say "(first taking [the noun]) ";
	silently try taking the noun;
	if the player is not holding the noun, stop the action.

Before putting something which is not carried by the player on something:
	if the noun is on the second noun, say "Already done." instead;
	say "(first taking [the noun])[line break]";
	silently try taking the noun;
	if the player is not holding the noun, stop the action.

Understand "put [things] in [something]" as inserting it into. Understand "put [things] on [something]" as putting it on.

The Closet is a room.

A lentil is a kind of thing. A black-eyed pea is a kind of thing. The closet contains 3 lentils. The Closet contains 14 black-eyed peas. The round tin is a container in the closet. The round tin contains 17 lentils. The square tin is a container in the Closet. The square tin contains 20 black-eyed peas.

Sorting is a scene. Sorting begins when play begins. Sorting ends when all the lentils are in the round tin and all the black-eyed peas are in the square tin. When Sorting ends, end the story finally.

When play begins: say "Thanks to your cruel stepmother, you're not going anywhere until the lentils and peas are sorted."

Test me with "put peas in square tin / put lentils in round tin".
```

