# Week 01: Regex and ELIZA
We covered the following topics in order
1. Regular Expressions
2. Basic ELIZA Understanding
3. Text-Normalization
   - Tokenization
   - Lemmatization (Stemming)
   - Sentence Segmentation
4. Edit Distance

# Regex and ELIZA

**Regular Expression** (*regex*) can be used to specify strings we might want to extract from a document.

A regular expression search function (in Python or Unix) will search through the corpus of texts, returning all texts that match the pattern. However, the examples in the following overview only show the first match.

It's important also to notice what we understand by **string**. In general, you have to see a string as any sequence of characters, and these characters can be alphanumeric, underscore, special chars, and even blank spaces. This is the general view when we talk about strings.

1. **Disjunctions**: 
   - Disjunctions are used to match a **single** character from a set of characters inside braces `[]`.
   - Example: `[wW]oodchuck` matches both "Woodchuck" and "woodchuck".
   - You can even use a range. For example, all the uppercase and lowercase chars would be `[A-Za-z]`

2. **Negation in Disjunction**: 
   - The caret symbol `^` is used inside square brackets to negate the set.
   - Example: `[^A-Z]` matches any character that is not an uppercase letter.

3. **More Disjunctions with Pipe**: 
   - The pipe symbol `|` is used for disjunction, which matches either of the expressions.
   - Example: `groundhog|woodchuck` matches either "groundhog" or "woodchuck".

4. **Optional, Zero or More, One or More, Any Character**: 
   - The symbols `?`, `*`, `+`, and `.` are used for optional characters, matching zero or more characters, matching one or more characters, and any character respectively.
   - Example: `colou?r` matches both "color" and "colour".
   - You can also define a range from n to m occurance using `{n,m}`

5. **Anchors**: 
   - Anchors like `^` and `$` are used to match the start and end of a line.
   - Example: `^[A-Z]` matches a line starting with an uppercase letter.
   - You can also use `\b` for word boundary and `\B` for non-word boundary. 
   - A **word** for a regular expression is defined as any sequence of digits, underscores, or letters.

6. **Parentheses and Capture groups**
   - Enclosing a pattern in parentheses `( )` makes it act like a single character. In other words, parentheses capture groups.     
      - For example: `gupp(y|ies)` to match guppy or guppies.
   - It is possible to reuse the matched patterns. When we use parentheses `()` the resulting match is store in a **numbered register**, which can be access with `\1`, `\2`, and so on.
      - Example: `the (.*)er they (.*), the \1er we \2`, which match *the faster they ran, the faster we ran* 
   - You can create a non-capturing group (with no register), using `?:` in `(?: pattern)`.

7. **Substitutions and Capture Groups**: 
   - Substitution syntax (like `s/regexp1/pattern/`) replaces matched patterns.
   - Additionally, it is possible to use `( )` during the substitution in order to capture groups and reuse matched patterns, as before.
   - Example: `s/([0-9]+)/<\1>/` adds angles around all numbers.

8. **Lookahead Assertions**: 
   - Lookahead assertions are powerful tools in regex that allow for conditional matching
     - `(?= pattern)` checks to see if the given pattern exists after the current point in the string.
     - `(?= pattern)` checks to see if the given pattern doesn't exist after the current point in the string.
     - In both cases, the regex engine **looks ahead** for the specified pattern, but the text matched by the lookahead is not included in the overall match. For that reason, we say it has **zero-width**.
   - Example: `ˆ(?!Volcano)[A-Za-z]+` matches any word at the start of a line that doesn’t start with "Volcano".
   - Example 2: The regex `q(?=u)` will match the letter 'q' only if it is immediately followed by the letter 'u'. In the string "quiet", it matches the 'q', but does not include the 'u' in the match. So, the overall match is just 'q'. Notice, it will not match the 'q' in the word 'Iraq'.

9. **Operator Precedence Hierachy**
   - In regular expression, one operator may take precedence over another. The following table depicts this order from higher to lowest precedence:

      |  | |
      |--------------|-------|
      |Parenthesis | `()` |
      | Counters | `*` `+` `?` `{}` |
      | Sequence and anchor | the `^`my end`$` `\b` |
      | Disjunction | `\|` |


Here's a table summarizing some of the above regex rules and examples:

| Regex Rule              | Example Pattern       | Example Match         |
|-------------------------|-----------------------|-----------------------|
| Disjunctions            | `[wW]oodchuck`        | Woodchuck, woodchuck  |
| Negation in Disjunction | `[^A-Z]`              | Any non-uppercase letter |
| Pipe for Disjunction    | `groundhog\|woodchuck`| groundhog, woodchuck  |
| Previous Optional Character     | `colou?r`             | color, colour         |
| Zero or More Characters | `oo*h!`               | oh!, ooh!, oooh!      |
| One or More Characters  | `baa+`                | baa, baaa, baaaa      |
| Exactly n Occurances    | `ba{n}` `ba{2}`       | baa (no 1 nor 3) |
| Exactly n to m Occurances    | `ba{n,m}` `ba{2,4}`       | baa, baaa, baaaa |
| Exactly at least n Occurances    | `ba{n,}` `ba{2,}`       | baa, baaa, baaaa, baaaaaaaaaaa |
| Any Character           | `beg.n`               | begin, begun, beg3n   |
| Start of Line Anchor    | `^[A-Z]`              | Any line starting with an uppercase letter |
| Capture Group (Twice in a string) | `(New York).*\1` | New York! Really in New York!? |
| Non-Capture Group | `(?:some\|a few) (people\|cats) like some \1` | some cats like some cats |
| Substitution            | `s/([0-9]+)/<\1>/`    | the 35 boxes → the <35> boxes |
| Lookahead Assertion (Conditional Matching)    | `ˆ(?!Volcano)[A-Za-z]+` | Matches a word at the start of a line not starting with "Volcano" |



## Application - ELIZA: 
Demonstrates how regex was used in the early NLP system ELIZA for pattern matching and responses.

The substitutions are used in the following example:

```
s/.* I’M (depressed|sad) .*/I AM SORRY TO HEAR YOU ARE \1/
s/.* I AM (depressed|sad) .*/WHY DO YOU THINK YOU ARE \1/
s/.* all .*/IN WHAT WAY/
s/.* always .*/CAN YOU THINK OF A SPECIFIC EXAMPLE/
```

## Special Cases to Take in Mind

### `^`, `$`, `\b` differences

1. `^` (caret) and `$` (dollar sign) anchors:
    - `^` is the caret symbol, and it represents the start of a line or string.
    - `$` is the dollar sign symbol, and it represents the end of a line or string.
    - They are used to specify that a pattern should match only at the beginning or end of a line or string, respectively.
2. `\b` word boundary anchor:
    - `\b` is a word boundary anchor, and it is used to specify a word boundary, but **it won't treat underscores and numbers** as word boundaries.
    - It allows you to match whole words, rather than just substrings.
    - `\b` is not limited to the start or end of a string; it can be used within the string to match word boundaries within text.


In summary, `^` and `$` anchors are used to specify the start and end of a line or string, respectively, while `\b` is used to match word boundaries within text.

---

### `re.findall()` in Python

`re.findall()` returns **all non-overlapping occurrences** of the pattern in the input string as a list of strings (or tuples of strings if there are capturing groups), and it continues searching for all matches throughout the entire string

---

### Other things in Notes
- False Positives and Fase Negatives
- Greedy and non-greedy matching
- Special Chars as `\s` blank space
- backslah used to referred to special char as `\n`, `\t` or `\*` (the ast).

