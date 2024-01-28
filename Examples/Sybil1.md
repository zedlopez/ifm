Example: * Sybil 1
Location: Reading and talking
RecipeLocation: Saying Simple Things
Index: Sybil 1. ASK, TELL, and ANSWER conflated
Description: Direct all ``ask``, ``tell``, and ``answer`` commands to ``ask``, and accept multiple words for certain cases.
For: Z-Machine

  
Sometimes we do not particularly want to deal with all the variations on asking, telling, or answering someone something, but want to direct everything to a single conversational command:

  

``` inform7
{*}"Consulting the Oracle"

The Grove is a room. In the Grove is a woman called the Sybil.

Instead of telling someone about something, try asking the noun about it. Instead of answering the noun that something, try asking the noun about it.

Instead of asking the Sybil about "persians", say "She nods gravely."
```

  
And similarly, a difference between ``give`` and ``show`` is sometimes overkill:

  

``` inform7
{**}Instead of showing something to someone, try giving the noun to the second noun.

The player carries a coin. Instead of giving the coin to the Sybil: move the coin to the Sybil; say "She accepts with a smile."
```

  
It is also often the case that we want to accept more than one form of a term. For instance

  

``` inform7
{**}Instead of asking the Sybil about "Darius/king", say "Her smile unnerves you."
```

  
will match either "Darius" or "king". If necessary, we can go a step further and define our own token to match a variety of phrases, like this:

  

``` inform7
{**}Understand "Athenians/Spartans/Greeks" or "hoplite army/forces" as "[Greeks]". Instead of asking the Sybil about "[Greeks]", say "She looks encouraging."
```

  
The token `"[Greeks]"` will match all of "Athenians", "Spartans", "Greeks", "hoplite army", or "hoplite forces". It will not match "hoplite" or "forces" alone; it is important to note that the / divides individual words which are understood equivalently, but does not define entire phrases as equivalent. More about how Inform understands specific phrases can be found in the chapter on [Understanding].

  

``` inform7
{**}Test me with "test one / test two".

Test one with "ask sybil about persians / tell sybil about persians / sybil, persians / ask sybil about darius / ask sybil about king".

Test two with "ask sybil about greeks / ask sybil about athenians / ask sybil about hoplite army / ask sybil about hoplite forces / give the coin to the sybil".
```

