Example: ** Laura
Location: Two descriptions of things
RecipeLocation: Varying What Is Read
Index: Printed names for complex-named objects
Description: Some general advice about creating objects with unusual or awkward names, and a discussion of the use of printed names.
For: Z-Machine

  
Occasionally it is useful to give something a printed name because we want to call it something extremely long-winded; give one thing a name that is the subset of the name of something else; or use words such as "with" or "and" that are likely to confuse Inform into thinking that the object name ends before it actually does.

  
Often it is enough to preface these ambiguously-titled things with "a thing called..." or "a supporter called..." or the like, as here:

  

``` inform7
South of Spring Rolls is a room called Hot and Sour Soup.
```

  
prevents Inform from trying to read "Hot and Sour Soup" as two separate rooms, while

  

``` inform7
The player carries an orange ticket. The player carries a thing called an orange.
```

  
creates two objects instead of the one orange ticket that would result if the second sentence were merely "The player carries an orange."

  
Really long names can be a bit cumbersome. For example:

  

``` inform7
The player carries a thing called an incriminating photograph of a woman with blonde hair.
```

  
So we might instead give the photograph a printed name:

  

``` inform7
{*}"Laura"

The City of Angels is a room. The incriminating photograph is carried by the player. The printed name of the incriminating photograph is "incriminating photograph of a woman with blonde hair".
```

  
Now we've gotten around any awkwardness with printing the name – but we also need to understand when the player refers to the photograph. When we define the names of objects under normal circumstances, Inform takes care of this automatically, but if we have especially set the printed name, we must also specially define the appropriate terms for the player to use. For this we need "understand", which will be explained in much more depth in a later chapter:

  

``` inform7
{**}Understand "woman" or "with" or "blonde" or "hair" or "of" or "a" as the incriminating photograph.

Test one with "x photograph / x incriminating photograph of a woman with blonde hair / x hair / x blonde / x woman with blonde hair / x incriminating photograph of a woman".
```

  
That's probably as far as we really need to go, and if you are satisfied with this behavior, there is no need to read on.

  
One possible objection to this solution is that Inform will accept some nonsensical formulations as applying to the photograph: for instance, it will allow >``examine photograph`` OF, >X ``blonde photograph woman incriminating``, or even >X OF ...though in the case there were two items with "of" names, the game would disambiguate with a question such as "Which do you mean, the incriminating photograph of a woman with blonde hair or the essence of wormwood?"

  
Traditionally, Inform has tended to be fairly flexible about word order, preferring to err in the direction of leniency. On the other hand, there are times when we need more exacting rules in order to distinguish otherwise similar cases.

  
Two features allow us to specify more exactly if we so desire. The first is that, if we specify a whole phrase as the name of something, all the words in that phrase are required, in the order given. Thus "Understand "blonde hair" as the photograph" would require that both "blonde" and "hair" be present, and would not recognize >X ``blonde``, >X ``hair blonde``, or >X ``hair``.

  
Second, we can create tokens, such as "Understand "blonde hair" or "hair" as `"[hair]"`, and then use these tokens in match phrases. This saves a good deal of time when we want to specify a number of different but fussy alternatives. So, for instance, here is a drawing that would not respond to >X OF, or >X ``brown eyes``, but would respond to >X ``drawing`` OF ``man with brown eyes``, >X ``man with brown eyes``, and so on:

  

``` inform7
{**}The drawing is carried by the player. The printed name of the drawing is "drawing of a man with brown eyes".

Understand "eyes" or "brown eyes" as "[brown eyes]". Understand "man" or "man with [brown eyes]" or "brown-eyed man" as "[man]". Understand "[man]" or "drawing of [man]" or "drawing of a [man]" as the drawing.

Test me with "test one / test two".

Test two with "x drawing / x man / x of / x drawing of man / x drawing of a man / x drawing of a man with brown eyes / x drawing of a brown-eyed man / x brown eyes".
```

  
Further refinements are possible: the "privately-named" attribute tells Inform not to try to understand the source name of an object at all, so if we write

  

``` inform7
The purple rabbit is a privately-named thing.
```

  
...the player will not be able to refer to it as "purple" or "rabbit" or "purple rabbit".

  
There are also ways to make names to refer to entire kinds of objects (so "dude" will refer to any man in the game); to specify names that only refer to objects in the plural (so ``get pictures`` will pick up several pictures together); to reflect an object's properties (so "red apple" works only as long as the apple is in fact red); or even to refer to the object's relationships to other objects (so "bottle of wine" works only when wine is indeed in the bottle). All these refinements are discussed in the chapter on Understanding.

