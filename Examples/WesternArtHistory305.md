Example: ** Western Art History 305
Location: Multiple action processing
RecipeLocation: Actions on Multiple Objects
Index: Allowing EXAMINE to see multiple objects with a single command
Description: Allowing EXAMINE to see multiple objects with a single command.
For: Z-Machine

  
In a gallery, there are many individual things to look at, but you can also get a general impression by just examining them as a collection.

  
First, we'll make a kind for the paintings exhibited in the gallery, and then we'll also make a special object to represent all of them as a mass:

  

``` inform7
{*}"Western Art History 305"

A painting is a kind of thing. A painting is usually fixed in place. Understand "painting" as a painting. Understand "paintings" as the plural of painting.

The painting-collective is a thing. The printed name of the painting-collective is "paintings". The description of the painting-collective is "There's [a list of visible paintings]."
```

  
We could if we wanted tweak the description to be different in style in different rooms of the gallery, but this will do for now. Next we need to make it possible to type something like ``examine paintings``, which normally wouldn't work because the Standard Rules don't tell Inform to recognise multiple objects with the ``examine`` command (unlike, say, ``drop`` or ``take``). This is easy:

  

``` inform7
{**}Understand "examine [things]" as examining.
```

  
Now to make use of the special object. If the player types ``examine paintings``, the multiple object list will become a list of the visible paintings. The following rule looks at this list: if it contains more than one painting, it replaces them with the painting-collective instead. Now there's only one examining action, so we get a reply like "There's an abstract painting, a pointilist painting and a French academic painting." instead of a list of descriptions of each in turn.

  

``` inform7
{**}A multiple action processing rule when the current action is examining (this is the examine kinds rule):
	let L be the multiple object list;
	let F be L;
	let the painting count be 0;
	repeat with item running through L:
		if the item is a painting:
			increment the painting count;
			remove the item from F;
	if the painting count is greater than one:
		add the painting-collective to F;
		alter the multiple object list to F.
```

  
And now some art to try this out on:

  

``` inform7
{**}Gallery is a room. "Various paintings hang on the walls of this gallery, awaiting critical attention. A side chamber to the north contains smaller works."

The abstract painting, the pointilist painting, and the French academic painting are paintings in the Gallery.

North of the Gallery is the Side Chamber. A handsome miniature is a painting in the Side Chamber. The description of the handsome miniature is "The miniature depicts a uniformed soldier of the late 18th century, with braid on his shoulders and a curl in his beard."

The player carries a small notebook. The description of the notebook is "It contains the notes you've taken so far towards a paper for Western Art History 305. So far you're still feeling a bit uninspired."

Test me with "x paintings / x all / n / x paintings / x all".
```

