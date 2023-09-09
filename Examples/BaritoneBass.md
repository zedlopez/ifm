Example: *** Baritone, Bass
Location: Understanding values
RecipeLocation: Traits Determined By the Player
Index: Allowing the player to describe the main character before starting play
Description: Letting the player pick a gender (or perhaps other characteristics) before starting play.
For: Z-Machine

  
The "reading a command" activity is rather advanced; for the moment, what we need to understand is that we're intervening in commands at the start of play and insisting that the player's first instruction to the game consist of a choice of gender. After that point, the gender will be set and play will proceed as normal.

  
In order to do the parsing, we define gender as a kind of value, and give several alternate names to each gender.

  

``` inform7
{*}"Baritone, Bass"

Getting Started is a room.

Gender is a kind of value. The genders are masculine, feminine, and unknown. Understand "male" or "man" or "M" as masculine. Understand "female" or "woman" or "F" as feminine.

A person has a gender. The gender of the player is unknown.

When play begins:
	now the command prompt is "Please choose a gender for your character. >".

After reading a command when the gender of the player is unknown:
	if the player's command includes "[gender]":
		now the gender of the player is the gender understood;
		if the gender of the player is unknown:
			say "This story requires a selection of male or female. [run paragraph on]";
			reject the player's command;
		if the gender of the player is masculine, now the player is male;
		if the gender of the player is feminine, now the player is female;
		say "[line break]Thank you. We now begin...";
		now the command prompt is ">";
		move the player to Sandy Beach;
		reject the player's command;
	otherwise:
		say "Sorry, we're not ready to go on yet. [run paragraph on]";
		reject the player's command.

Sandy Beach is a room.

Instead of examining the player when the player is female:
	say "Congratulations, you are a girl!"

Instead of examining the player when the player is male:
	say "Congratulations, you are a boy!"
```

  
If we had a whole series of things to ask the player about, we might define a whole series of kinds of value

  

``` inform7
The vocal ranges are soprano, mezzosoprano, contralto...
```

  
and use a "construction stage" variable to keep track of the current stage of character-construction, as in

  

``` inform7
After reading a command when the current construction stage is choosing a vocal range:
	...
```

