Example: * Numberless
Location: Otherwise
RecipeLocation: Varying What Is Written
Index: Otherwise if demonstrated
Description: A simple exercise in printing the names of random numbers, comparing the use of "otherwise if...", a switch statement, or a table-based alternative.
For: Z-Machine

  

``` inform7
{*}"Numberless"

The Rambling Warren is a room.

When play begins:
	let N be a random number between 1 and 5;
	if N is 1:
		say "N is one.";
	otherwise if N is 2:
		say "N is two.";
	otherwise if N is 3:
		say "N is three.";
	otherwise:
		say "N is more than the number of your toes."
```

  
The final "otherwise" here will fire only if none of the earlier conditions applies; we could leave it out and print nothing in the case that N is 4 or 5.

  
The more compact way to do this is to create a list of values that our number could match; in many programming languages this is called a switch statement. For example:

  

``` inform7
{**}When play begins:
	let Y be a random number between 6 and 10;
	if Y is:
		-- 6: say "Six is the magic number!";
		-- 7: say "The number of the day is seven!";
		-- otherwise: say "Today's magic number is boring."
```

  
As a final option, we can use a construction we've seen only briefly before now: a table. The use of [Tables] will be explained more fully in their own chapter, but here we see in brief that we can assign a number of values to one column of a table and then use that table to look up output:

  

``` inform7
{**}When play begins:
	let X be a random number between 11 and 14;
	if X is a number listed in the Table of Switching, say "[output entry][paragraph break]";
	otherwise say "X is greater than the number of your noses!"

Table of Switching
number	output
11	"X is eleven!"
12	"X is twelve!"
13	"X is thirteen!"

Test me with "z".
```

  
As we shall see, things other than text can be stored in tables, so we could also use a table as a way to look up objects or even rules to carry out.

