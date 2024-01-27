Example: *** Formal syntax of sentences
Location: What sentences are made up from
RecipeLocation: Information Only
Index: Formal syntax of sentences
Description: A more formal description of the sentence grammar used by Inform for both assertions and conditions.
For: Untestable

[ZL: numerous stylistic decisions made here; please review.]::

An entire grammar for the whole mass of Inform would not be linguistically interesting: it contains many convenient wordings which are not really part of a grand pattern. Inform does, however, have a formal notion of a Sentence, a grammatical structure which we shall call **S**. It is almost true that conditions ("if the flowerpot is on the wall") have the same grammar as assertions ("The flowerpot is on the wall") and "now" phrases ("now the flowerpot is on the wall"). All three use the ***S** grammar*, so we could define an assertion as "**S.**", say that "if **S**", "while **S**", "when **S**" and so on are conditions, and say that "now **S**" defines the "now" declaration.

[ZL: maybe "phrase" instead of "declaration" above to avoid muddying the water? ]::

  
Grammatical sentences do not necessarily make sense, of course. Many perfectly grammatical assertions in fact give rise to problem messages:

|Sentence|Message|
|---|---|
| `The wicker basket is not in the kitchen` | *Unhelpfully negative.* |
| `The wicker basket has been in the kitchen` | *Talks about a time which never existed.* |
| `The wicker basket is full` | *Full of what? Too vague.* |
| `The wicker basket is the ginger cat` | *Demonstrably false.* |

  
Whereas the first three, at least, would be sensible as conditions. So saying that assertions are "just like" conditions is a little misleading: what they have in common is S, the underlying grammar they each use as a starting-point.
  
To define **S**, we break it up into subsidiary structures. The most important is the **Description Phrase (DP)**, examples of which include "the red basket", "somewhere lighted" and "an empty open container". Clearly sentences include **DP**s, but they also include other ingredients. The general pattern used in Inform is very simple:

1. **S** = **DP** + **VP**
2. **VP** = **Verb** + **DP**
  
where VP is another structure, the Verb Phrase. Consider the sentence `the horseman wears a riding helmet`:

> **S** (`the horseman wears a riding helmet`) = **DP** (`the horseman`) + **VP** (`wears a riding helmet`)
>
> **VP** (`wears a riding helmet`) = **Verb** (`wears`) + **DP** (`a riding helmet`)
  
In that example, the **Verb** was the single word "wears". More generally, Inform allows a **Verb** to include adverbs and prepositions, to be negated, and to come in any of four tenses, so the following are all valid examples of **Verb** in our grammar:

- `wore`
- `carries`
- `is carried by`
- `had not been inside`
  
Although we are not going through the definition of **Description Phrases** in detail, it is worth noticing how "which" and "who" behave:

3. - **DP** = **DP** + which + **VP**
   - **DP** + who + **VP**
  
Thus `an open container which is in the Ballroom` can be broken down as:

> **DP** (`an open container`) + which + **VP** (`is in the Ballroom`)
  
To understand compounds like "something in a container", we have to invent a new grammatical structure for `in a container` and similar: let's call this a **Relative Phrase (RP)**.

4. **DP** = **DP** + **RP**
  
Thus `an open container in the Ballroom` is **DP** (`an open container`) + **RP** (`in the Ballroom`). **Relative Phrases** have two different forms:

[ZL: The absence of any real definition of Preposition confused me for a long time. I think it would be enormously more clear to just say that bothe of these *are the same case* and that case is "anything following 'to be' in a verb." Clearer still if the docs said out loud somewhere that passive voice "to be Xed by" verbs are automatically created as the reversed relation for any single-word X verbs corresponding to a (non-reversed) relation.]::

5. - **RP** = **Preposition** + **DP**
   - **RP** = **Participle** + **DP**
  
`in a container` is an example of the former. An example of the latter would be

> **RP** (`worn by Mr Darcy`) = **Participle** (`worn by`) + **DP** (`Mr Darcy`)
  
That is nearly it, but not quite: we must go back to the "almost" in the statement above that assertions and conditions "almost" have the same grammar **S**. The difference arises from a curious irregularity in English called subject-verb inversion (see the *Oxford English Grammar* at 3.22F), whereby assertions can be reversed but not conditions.

Take `In the Garden is a sunflower`: this does not follow the pattern **S** = **DP** + **VP**, because "in the garden" is not a **DP**: indeed, it is not a noun at all. To make sense of this sentence, Inform reverses it to "A sunflower is in the Garden", which does indeed follow **DP** + **VP**. Hence, the final rule:

6. **S** = **RP** + **Verb** + **DP** [assertions only]
  
So the condition "if in the garden is a sunflower..." fails because rule 6 does not apply to the grammar for conditions: while occasional poetic uses of subject-verb inversion do turn up in conditions ("If On A Winter's Night A Traveller", say), they are rare in ordinary English usage, and illegal in Inform.

That completes the **S** grammar, so to recap:

1. **S** = **DP** + **VP**
2. **VP** = **Verb** + **DP**
3. - **DP** = **DP** + which + **VP**
   - **DP** + who + **VP**
4. **DP** = **DP** + **RP**
5. - **RP** = **Preposition** + **DP**
   - **RP** = **Participle** + **DP**
6. **S** = **RP** + **Verb** + **DP** [assertions only]
