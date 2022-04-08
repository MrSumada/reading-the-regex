# Reading the Regex

You see them all around you, Regex Expressions.  The shockingly pervasive, seemingly nonsensical series of slashes, letters, numbers, and odd characters have found themselves relevant since the 1950s, and can be utilized in every common programming language.  Luckily these expressions only seem haphazard on first glance, and with a little core information the pattern and power behind the characters can come through. This guide is here to demystify everything from /[a-zA-Z0-9!@#$%^&*(){}]/ to /./

## Summary

To put is simply, a Regex or "regular expression" is a series of special characters that can check a string for matches that meet certain requirements. This guide will delve into what those special characters are exactly, and how we can easily read them.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

Anchors in a regex expression determine how a string should begin or end.

    ^ --- A string will begin with the characters that follow the ^.
    $ --- A string will end with the characters that precede the $.
    \A --- A match must occur at the start of a string.
    \Z --- A match must occur at the end of a string or before a new line \n.
    \z --- A match must occur at the end of a string.
    \G --- A match must occur at the point where a previous match ended.
    \b --- A match must match positions between a alphanumeric or "word" character and a non-alphanumeric character.
    \B --- A match must NOT match positions between a alphanumeric or "word" character and a non-alphanumeric character.


### Quantifiers

Quantifiers appear after the string pattern and they set the limits that a string must fulfill to be matched.  This often pertains to the number of characters a string can be. 

    * --- Matches a pattern 0 or more time.
    + --- Matches a pattern 1 or more times.
    ? --- Matches a pattern 0 or 1 time only.
    { n } --- Matches a pattern exactly n times
    { n, } --- Matches a pattern at least n times
    { n, x } --- Matches a pattern at least n times, but no more than x times.

### OR Operator

The OR operator is often paired with grouping constructs, which normally find only exact matches.  Using the | or the OR operator, the matches can now be any rearrangement of the separated characters. For example (act) would only match "act", but (a|c|t) would match "act", "cat", "tac", etc. 

### Character Classes

Character classes simply define a se of characters.  There are some common character classes that can efficiently represent some pretty large groups!

    [characters] --- Matches any single character in the character group.
    [^characters] --- Matches exclude any single character in the character group.
    . --- Matches any character (except a newline character \n).
    \d --- Matches any arabic numeral (0-9).
    \w --- Matches any basic Latin alphanumeric including _.
    \s matches a single whitespace “ “, including tabs and line breaks.

And \D, \W, \S invert their corresponding lower case counterparts.  For example, \D would match occurrences that DON'T contain arabic numerals.

### Flags

After a regex literal expression is terminated with its second /, more functionality or limits can be added with a flag. Here are some common examples:

    g --- the global search, teh expression will test against all matches.
    i --- the characters' case should be ignored in matches.
    m --- the multi-line search, multi-line input strings should be treated as such.

### Grouping and Capturing

We can break larger search patterns into smaller "grouping constructs" or "subexpressions".  They allow us to break up larger open-ended regular expressions and thus have a greater degree of specificity and an ability to fulfill particular requirements. We designate groupings with parentheses () and they are unique is a couple ways. 

First off the find exact matches. So (Hello) will match "Hello" but not a rearrangement like "Helol". 

Secondly, they benefit from an OR operator that allows these exact match searches to match with rearranged
variations.  For example (act) would only match "act", but (a|c|t) would match "act", "cat", "tac", etc. 

And finally, subexpressions can be either "Capturing" or "Non-Capturing". Capturing subexpressions can "capture" sequences for eventual reuse, whereas non-capturing subexpressions do not.  A subexpression can be deemed non-capturing by adding ?: to the beginning of the parentheses like so (?:act).

    ( sub ) --- captures match and assigns a number.
    (?< name > sub ) or (?' name ' sub) --- captures match and assigns a named group.
    (?: sub ) --- defines a non-capturing group.

### Bracket Expressions

Bracket expressions or a "positive character group" use [] to represent a range of characters that can fulfill the requirements. For example [abcde] will match any combination of those letters, from "abba" to "ecce" to "baccade". Bracket expressions may also use a hyphen (-) to connect sequential characters like [a-z] or [0-9]. In fact, that [abcde] could have been written [a-e]!

Characters and hyphenated ranges of characters can be written adjacent in bracket expressions, and anything included in the expression will be sought in matches.  A bracket expression could look like [abcde12345] or [A-Z0-9?!] or [13579-+=/].  Just know that special characters must be written after the alphanumeric characters. 

It's also worth noting, that regex is case-sensitive, so a bracket expression of [a-z] would not match "Hello" due to the capital "H".  However, because adjacent ranges can be combined in regex, [a-zA-Z] would match all upper and lower case characters, including "Hello". So these 

Finally a bracket expression can be flipped into a negative, meaning that everything in the expression will be excluded, not included in the matches. This is done using a ^ at the beginning of the bracket expression. So [^a-z] would exclude all lower case letters from matches.

### Greedy and Lazy Match

Whether a regex expression is greedy or lazy pertains to the number of matches it will attempt to make.
The quantifier for searches is inherently greedy, meaning it will match as many occurrences as possible. Whereas a lazy quantifier will match only the minimum number of occurrences.

Quantifiers can be made lazy by having a ? follow them. 

### Boundaries

Word Boundaries are specific anchors that match positions between a alphanumeric or "word" character and a non-alphanumeric character. It's designated by \b. Similarly, we can use \B on  matches that do NOT occur on a boundary.

### Back-references

Backreference allow previously matched subexpressions to be identified later in the same regex. This would commonly be used for finding repeated words for example. Backreference constructs can be either number or name constructs. 
\number match the value of a numbered subexpression. 
\k< name > matches the value of a named subexpression.

### Look-ahead and Look-behind

Lookarounds in regex match occurrences if their surrounds also match a specified substring. 

    reg(?=sub) --- matches if "reg" is immediately followed by "sub".
    reg(?!sub) --- matches if "reg" is NOT immediately followed by "sub".
    (?<=sub)reg --- matches if "reg" is immediately preceded by "sub".
    (?<!sub)reg --- matches if "reg" is NOT immediately preceded by "sub".


## Author

This guide was written by Adam Payne, a web designer, film producer and editor, motion graphics designer, and improv actor based out of Brooklyn, New York. You can find some his work on his github here: https://github.com/MrSumada/
