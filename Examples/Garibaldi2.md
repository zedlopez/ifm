Example: * Garibaldi 2
Location: Text with type styles
RecipeLocation: Typography
Index: Garibaldi 2. Coloured text styles
Description: Adding coloured text to the example of door-status readouts.
For: Z-Machine

  
The extension "Basic Screen Effects" provides a few more type styles, in the form of coloured lettering. The colours available are red, yellow, green, blue, white, magenta, and cyan, as well as the usual black; and to restore the player's default screen colour, we say "default letters".

  
Thus if we wanted to highlight locked and unlocked doors in our security readout example:

  

``` inform7
{*}"Garibaldi"

Include Basic Screen Effects by Emily Short.

The security readout is a device. The description of the readout is "The screen is blank."

Instead of examining the switched on security readout:

	say "The screen reads: [fixed letter spacing]";

	say line break;

	repeat with item running through doors:

		say line break;

		say "  [item] ([front side of the item]/[back side of the item]): [if the item is locked][green letters]LOCKED[default letters][otherwise][red letters]UNLOCKED[default letters][end if]";

	say variable letter spacing;

	say paragraph break.

The player carries the security readout.

The Docking Bay is a room. The inner airlock is a door. It is north of the Docking Bay and south of the Zocalo. The inner airlock is lockable and unlocked.  The outer airlock is lockable and locked. It is a door. It is south of the Docking Bay and north of Space.

The quarantine seal is a door. It is west of the Zocalo and east of Medlab. Quarantine seal is locked.

The security pass unlocks the inner airlock. The player carries the security pass.

Test me with "x readout / turn on readout / x readout / lock inner airlock with security pass / x readout".
```

  
Note that this extension does not currently produce the desired effects when compiling with the Glulx setting; to see it working, make sure that the settings tab is set to compile to the Z-machine.

