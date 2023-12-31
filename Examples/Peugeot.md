Example: * Peugeot
Location: Vehicles and pushable things
RecipeLocation: Bicycles, Cars and Boats
Index: Travel requiring a vehicle
Description: A journey from one room to another that requires the player to be on a vehicle.
For: Z-Machine

  
Let's say that our protagonist is about to flee . Obviously, they can't make the journey on foot; they need transportation.

  

``` inform7
{*}"Peugeot"

Include Rideable Vehicles by Graham Nelson.

The Lot is a room. The ten-speed bike is a rideable vehicle in the Lot.
```

  
We make the ten-speed bike a rideable vehicle because we want to say that the player is on it rather than in it. Then our other room:

  

``` inform7
{**}Cambridge is east of the Lot.
```

  
And now we borrow from the Actions chapter to prevent travel without the proper equipment:

  

``` inform7
{**}Instead of going to Cambridge when the player is not on the ten-speed bike:
	say "It's a long journey to Cambridge: you'll never make it on foot."

After going to Cambridge:
	say "You begin pedalling determinedly.";
	continue the action.

Test me with "e / get on ten-speed bike / e".
```

