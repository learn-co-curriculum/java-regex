# Regular Expressions

## Learning Goals

- Learn what a regular expression is.
- Learn how to use the regex notation.

## What is a Regular Expression?

A **regular expression** (or **regex** for short) is a sequence of characters
that forms a search pattern. These expressions are helpful when we want to
validate input from a user! For example, if we want the user to create a strong
password that includes uppercase characters, lowercase characters, numbers, and
special characters and also be at least 8 characters long, then we could easily
verify a strong password using regular expressions!

A regular expression describes a pattern in text. A pattern could be looking for
a specific word, a grouping of words, punctuation, and white space. In a general
sense, we can look for certain formats using regex. For example, looking for a
phone number with the format (XXX) XXX-XXXX. Before we even incorporate regex
into some Java code, we will look at some syntax along with a useful tool to
help us further our understanding!

## Regex 101

Regular expressions aren't always the easiest to learn and can be hard to read
even for a seasoned programmer. Click on the link below to take you to tool
called Regex 101:

[Regex 101](https://regex101.com/)

When you get to the page, you will see a text box for you to enter your regular
expression and another text box where you can enter a test string. On the
right-hand side, you will see an explanation box, a match information box, and
even some quick references of various tokens that can be used with regular
expressions. This is an extremely helpful tool when you want to write regular
expressions, and you'd like to test them first before even writing them in your
code. It is advised you use this tool as you go through these next few lessons
to help you understand exactly what the regex evaluates to and how to improve
your own regular expressions when writing them in the future.

To get started using Regex 101, go ahead and change the "Flavor" to Java 8 since
we will eventually be using regular expressions with Java. You can also go ahead
and click on the "gm" in the far right of the "Regular Expression" text box and
turn off the "multi line" flag for now as well.

Your screen should now look like this:

![Regex-Java-Global](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/Regex101.png)

Again, try to follow along with the rest of this lesson using Regex 101 to help
understand the syntax a little bit better.

## Regex Syntax

In its simplest form, a regex can look for an exact literal piece of text. For
example, if given the sentence:

```plaintext
Twinkle twinkle little star, how I wonder what you are.
```

If we were to provide a regular expression of "star", it would find the literal
word `star` in the above sentence. If we decided to look for the pattern of
"ar", then it would find the characters "ar" in `star` and `are`.

Pretty simple, huh? Let's look at some metacharacters now to start showing
just how powerful regular expressions can be.

### Metacharacters

Remember how we learned about escape sequences in the last module in the
Characters and Strings lesson? Well guess what - our friend, the backslash,
'\', is coming back to help us with regular expressions! Consider the table
below of predefined metacharacters:

| Metacharacter | Description                          |
|---------------|--------------------------------------|
| `.`           | Matches any character                |
| `\s`          | Matches any whitespace character     |
| `\S`          | Matches any non-whitespace character |
| `\d`          | Matches any digit                    |
| `\D`          | Matches any non-digit                |
| `\w`          | Matches any word character           |
| `\W`          | Matches any non-word character       |

As we can see from the table above, case is crucial - so make sure if you are
looking for a digit that it is a lowercase 'd' and not an uppercase 'D'!

Let's look at some examples to showcase these metacharacters. In the Regex 101
tool, provide the following test string:

```plaintext
September 15th is National Online Learning Day!
```

#### The dot (.)

The special character `.` will match any single character. Let's enter the
pattern `"."` in the "Regular Expression" text box in Regex 101. Notice how
every single character, including the whitespace and punctuation is highlighted!

Time to be a little more specific and narrow our search using the `.`. In the
"Regular Expression" text box in Regex 101, let's change the pattern to `".s"`
and see what happens now.

```plaintext
is
```

We only have one match now! The pattern `".s"` evaluates to "Find me all the
places in the string where there is exactly 1 character before the character s."
Given our example test string, it will only match the pattern with "is".

Let's change it up one more time before we move onto the next metacharacter. In
the "Regular Expression" text box in Regex 101, change the pattern to `"..a"`.

```plaintext
 Na
ona
Lea
 Da
```

This time we have 4 matches. The pattern `"..a"` evaluates to "Find me all the
places in the string where there is exactly 2 characters before the character
a." Given our example test string, the pattern will match with the four
substrings. Notice how it even captured the space character in the two matches!

#### Whitespace and Non-Whitespace

The special character `\s` will match a literal space character ' ', a tab
(`\t`), a newline character (`\n`), or a carriage return (`\r`). The special
character `\S` does the inverse and will match any character _except_
whitespace. Let's enter the pattern `"\s"` in the "Regular Expression" text box
in Regex 101. Notice how all the spaces are highlighted. Now change the regular
expression to `"\S"` and see every other character _except_ the spaces
highlighted.

Now modify the test string to this:

```plaintext
September 15th
is National Online Learning Day!
```

Now enter in `"\s"` again into the regular expression text box and see how the
pattern matches with the carriage return character!

#### Digit and Non-Digit

The special character `\d` will match any digit 0-9 whereas the special
character `\D` does the inverse and will match any character _except_ a digit.
Let's return to our Regex 101 tool and enter the pattern `"\d"` in the
"Regular Expression" text box. Notice how the digits `1` and `5` are
highlighted. Now change the regular expression to `"\D"` and see every other
character _except_ the two digits.

Say we want to find a two-digit number now. We could enter `"\d\d"` into the
"Regular Expression" text box then. Now instead of two matches, we only get one
match of `15` since we are specifying in our pattern that it must be a two-digit
number.

#### Word and Non-Word

The special character `\w` will match a "word" character. A "word" character is
considered an uppercase letter (A-Z), a lowercase letter (a-z), any digit 0-9,
and the underscore character (_). The special character `\W` does the inverse
and will match any character_except_a word character. Let's enter the pattern
`"\w"` in the "Regular Expression" text box in Regex 101. Notice how all the
characters _except_ the whitespace characters are highlighted. Now change the
regular expression to `"\W"` to see all the whitespace characters highlighted.

### Character Sets

Maybe we want to match specific characters in a string though. Perhaps we want
to just find the vowels. For this, we can use the square brackets `[]` notation.
For example, the pattern `"[aeiou]"` will match any single character that is
part of that character set. Let's try entering that in Regex 101 as the pattern.

![regex-vowels](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-vowels.png)

Notice that only the characters between the square brackets is highlighted as a
match.

Now let's say we want to specify a range of characters. For example, maybe we
only want to find the characters that are letters. We can use the `-` between
two characters to represent a character range. Try entering the following
pattern into Regex 101 as a regular expression: `"[A-Za-z]"`.

![regex-letters](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-letters.png)

The pattern `[A-Za-z]` defines a character set containing all uppercase and
lowercase letters using the `-` to specify a range. If we want only uppercase
letters, we could change the pattern to be `[A-Z]` then or if we only want
lowercase letters, we could use the pattern `[a-z]`. We could even use this
syntax with numbers! `[0-9]` would be a pattern we could use to get any digit
between 0-9, which would be the same as using the shorthand `\d` character.

When looking at the metacharacters above, we saw there was usually an inverse.
(Like `\d` representing digits and `\D` representing every other character
except for digits.) Can we do the same thing with character sets? The answer is
yes, and we can use the carat, `^`, inside the square bracket notation to help
us out! Try entering the pattern `"[^A-F]"` into the "Regular Expression" text
box. This will match any character _except_ for uppercase letters A, B, C, D, E,
and F. This includes spaces, numbers, just any character as long as it is not in
the character set we specified. In the example above, we can see that every
character seems to be highlighted _except_ for the `D` character.

![regex-without-letters-A-F](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-no-D.png)

### Anchors

An **anchor** in regex allows us to specify the relative location of a pattern
match. The anchors we will look at are the carat symbol, `^`, and the dollar
sign symbol, `$`.

To help us truly look at how anchors work, let's change our "Test String" in
Regex 101 to the following:

```plaintext
A rose is a rose is a rose
```

Now let's enter the pattern `"[Aa] rose"` into the "Regular Expression" text box
and see what happens.

We get three matches since we are looking for either the character `A` or `a`
followed by a space and then the word `rose`:

```plaintext
A rose
a rose
a rose
```

Let's modify the pattern now and enter `"^[Aa] rose"` into the "Regular
Expression" text box. Notice how only the first part of the test string is now
a match! The `^` in this context is an anchor that says "Only check to see if
the pattern exists at the start of the string." Since it does, it will only
return `A rose` and not the other two matches.

Try to use the `^` anchor again by typing in `"^is"` in the "Regular Expression"
text box now. Even though the character combination of `is` exists in the
string, it will not show a match since it is not in the beginning of the test
string. If we were to remove the anchor, `^`, we would then have two matches.

The other anchor, `$`, will only check to see if the pattern exists at the end
of the string - so the opposite of the `^` anchor! Let's put this to use and
enter the pattern `"[Aa] rose$"` into the "Regular Expression" text box. Again,
see how we only have one match, and it is matching with the last `a rose` in the
test string this time! This is because it is at the end of the string.

### Quantifiers

The last syntax we will discuss is quantifiers. **Quantifiers** are regex
operators that can count the number of occurrences of a character. Consider the
table below:

| Quantifier | Description                      |
|------------|----------------------------------|
| `*`        | Matches zero or more occurrences |
| `+`        | Matches one or more occurrences  |
| `?`        | Matches zero or one occurrence   |

Let's look at some examples to showcase these quantifiers. In the Regex 101
tool, replace the test string with the following:

```plaintext
Hmm that is interesting that hummingbirds can fly backwards
```

### The "Any" Quantifier

The "any" quantifier is the asterisk, `*`, quantifier. If we place a `*` after
any character or character set, we will match with zero or more occurrences of
that character. Let's look at an example to help explain this more. In the
"Regular Expression" text box, enter the pattern `"[Hh]m"`.

We get only one match since we are looking for either the character `H` or `h`
followed by a space and the character `m`:

![no-quantifiers](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-no-quantifiers.png)

Now let's update the pattern to have an asterisk, `*`, follow the character `m`:
`"[Hh]m*"`.

![any-quantifier](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-any-quantifier.png)

Notice now that there are now 4 matches! The pattern `[Hh]m*` has been modified
to say "Find me all occurrences where there is either an `H` or `h` followed by
zero or more occurrences of the character `m`." This resulted into finding all
the lowercase `h` characters in the test string along with the character
sequence of `Hmm`. Since `Hmm` has two occurrences of `m`, the `*` quantifier
will pick up both `m` characters.

### The "Some" Quantifier

The "some" quantifier is represented by the `+` symbol. If we place a `+` after
any character or character set, we will match with one or more occurrences of
that character. Let's try entering the pattern `"[Hh]m+"` now into the "Regular
Expression" text box:

![some-quantifier](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-some-quantifier.png)

There is now only one match and that is the character sequence of `Hmm`. Notice
how the `+` quantifier picked up both `m` characters. This is because we are
now requiring the `m` character to be present at least once. It will grab any
other `m` characters following it as well since it fits the definition of the
"some" quantifier.

### The "Optional" Quantifier

The "optional" quantifier, `?`, allows exactly zero or one occurrence of a
character or character set. Let's see it in action! Enter the pattern `"[Hh]m?"`
into the "Regular Expression" text box:

![optional-quantifier](https://curriculum-content.s3.amazonaws.com/java-mod-3/regex/regex-optional-quantifier.png)

There is, again, 4 matches of the above pattern! This may look very similar to
the resulting matches from when we used the `*` quantifier, but look closer.
The rule is now to find all occurrences where there is either an `H` or `h`
followed by zero or one occurrence of the character `m`. This found all the
lowercase `h` characters again in the test string but only picked up the
sequence `Hm` instead of `Hmm` this time. Since `Hmm` has two occurrences of
`m`, the `?` quantifier will only pick up the first `m` character.

## Resources

- [Regex 101](https://regex101.com/)
