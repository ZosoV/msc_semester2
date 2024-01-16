# Regex and ELZA

"Basic Text Processing" presentation provides an overview of various regular expressions (regex) and their applications.

1. **Regular Expressions Disjunctions**: 
   - Disjunctions are used to match a single character from a set of characters.
   - Example: `[wW]oodchuck` matches both "Woodchuck" and "woodchuck".

2. **Negation in Disjunction**: 
   - The caret symbol `^` is used inside square brackets to negate the set.
   - Example: `[^A-Z]` matches any character that is not an uppercase letter.

3. **More Disjunctions with Pipe**: 
   - The pipe symbol `|` is used for disjunction, which matches either of the expressions.
   - Example: `groundhog|woodchuck` matches either "groundhog" or "woodchuck".

4. **Optional, Zero or More, One or More, Any Character**: 
   - The symbols `?`, `*`, `+`, and `.` are used for optional characters, matching zero or more characters, matching one or more characters, and any character respectively.
   - Example: `colou?r` matches both "color" and "colour".

5. **Anchors**: 
   - Anchors like `^` and `$` are used to match the start and end of a line.
   - Example: `^[A-Z]` matches a line starting with an uppercase letter.

6. **Substitutions and Capture Groups**: 
   - Substitution syntax (like `s/regexp1/pattern/`) replaces matched patterns.
   - Capture groups `( )` capture and reuse matched patterns.
   - Example: `s/([0-9]+)/<\1>/` adds angles around all numbers.

7. **Lookahead Assertions**: 
   - Lookahead assertions `(?= pattern)` match a pattern only if another pattern follows it.
   - Example: `/ˆ(?!Volcano)[A-Za-z]+/` matches any word at the start of a line that doesn’t start with "Volcano".

8. **Application - ELIZA**: 
   - Demonstrates how regex was used in the early NLP system ELIZA for pattern matching and responses.

Here's a table summarizing some of these regex rules and examples:

| Regex Rule              | Example Pattern       | Example Match         |
|-------------------------|-----------------------|-----------------------|
| Disjunctions            | `[wW]oodchuck`        | Woodchuck, woodchuck  |
| Negation in Disjunction | `[^A-Z]`              | Any non-uppercase letter |
| Pipe for Disjunction    | `groundhog\|woodchuck`| groundhog, woodchuck  |
| Optional Characters     | `colou?r`             | color, colour         |
| Zero or More Characters | `oo*h!`               | oh!, ooh!, oooh!      |
| One or More Characters  | `baa+`                | baa, baaa, baaaa      |
| Any Character           | `beg.n`               | begin, begun, beg3n   |
| Start of Line Anchor    | `^[A-Z]`              | Any line starting with an uppercase letter |
| Substitution            | `s/([0-9]+)/<\1>/`    | the 35 boxes → the <35> boxes |
| Lookahead Assertion     | `/ˆ(?!Volcano)[A-Za-z]+/` | Matches a word at the start of a line not starting with "Volcano" |


1. `^` (caret) and `$` (dollar sign) anchors:
    - `^` is the caret symbol, and it represents the start of a line or string.
    - `$` is the dollar sign symbol, and it represents the end of a line or string.
    They are used to specify that a pattern should match only at the beginning or end of a line or string, respectively.
2. `\b` word boundary anchor:
    - `\b` is a word boundary anchor, and it is used to specify a position between a word character (alphanumeric or underscore) and a non-word character (anything that is not alphanumeric or underscore).
    - It allows you to match whole words, rather than just substrings.
    - `\b` is not limited to the start or end of a string; it can be used within the string to match word boundaries within text.


In summary, `^` and `$` anchors are used to specify the start and end of a line or string, respectively, while `\b` is used to match word boundaries within text.

----

`re.findall()` returns all non-overlapping occurrences of the pattern 
in the input string as a list of strings (or tuples of strings if there are 
capturing groups), and it continues searching for all matches throughout the entire string

----

`\s` white space