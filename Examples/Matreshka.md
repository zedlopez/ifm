Example: * Matreshka
Location: Begin and end
RecipeLocation: Looking Under and Hiding
Index: SEARCH [room] action that opens every visible unlocked container
Description: A SEARCH [room] action that will open every container the player can see, stopping only when there don't remain any that are closed, unlocked, and openable.
For: Z-Machine

  

``` inform7
{*}"Matreshka"

Ransacking is an action applying to one thing.

Check ransacking:
	if the noun is not the location, say "You can hardly search [the noun] from here." instead.

Carry out ransacking:
	while the player can see a closed openable unlocked container (called target):
		say "[target]: [run paragraph on]";
		try opening the target.

Report ransacking:
	say "You can see nothing further worth searching."

The Russian Gift Shop is a room. In the Russian Gift Shop is a large wooden doll. It is closed and openable. In the large wooden doll is a medium wooden doll. It is closed and openable. In the medium wooden doll is a small wooden doll. It is closed and openable. In the small wooden doll is a tiny solid wooden doll.
```

  
And now we need to borrow from a later chapter for the command that will make this work:

  

``` inform7
{**}Understand "search [any visited room]" as ransacking.

Test me with "search gift shop".
```

