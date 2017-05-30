# All Languages

This document outlines general coding standards and conventions, regardless of
the language or technology. The should be viewed as an outline, and might be
superseded by language-specific rules, features, or limitations.

## File Structure

###### Encoding

Files will be encoded in UTF-8.

###### Line endings

Files will only use Unix-style line breaks (`\n`). When developing on a
non-POSIX platform (i.e. Windows), Git's `autocrlf` setting will be configured
to ensure that files checked into source control only contain line break
characters. See the [Version Control](VersionControl.md#coreautocrlf)
documentation for details.

## Whitespace, Line Breaks, and Empty Lines

Line structure &mdash; the way lines are laid out and broken up &mdash; is
critical for making the code readable and understandable. Whitespace should be
used judiciously, where allowed, to help the reader follow the code.

###### Tabs

Tabs **_must not_** be used for indentation in source or configuration files,
_unless_ they are required by the syntax of the file.

_Rationale:_ Not all systems and editors represent tabs in the same way. To
ensure consistency for readers, no matter what their platform or editor/viewer,
**always** use spaces for indentation.

###### Empty Lines

Empty lines **should** be used whenever possible to visually group sections of
code together (whether the section is syntactic or logical).

However, too many empty lines make the code difficult to follow &mdash; the
whitespace becomes distracting. Generally, the number of empty lines should be
limited to 1, maybe 2, depending on the language and construct.

_Rationale:_ Code that is too visually dense is difficult for a reader to
follow. Nothing stands out, so the eye cannot quickly scan for something
specific. Code that is too visually sparse suffers in a similar way.

## Comments

See [Comments documentation](Comments.md).

## Camel Case

_Copied from Google's
[Java style guide](https://google.github.io/styleguide/javaguide.html#s5.3-camel-case):_

> Sometimes there is more than one reasonable way to convert an English phrase
> into camel case, such as when acronyms or unusual constructs like "IPv6" or
> "iOS" are present. To improve predictability, Google Style specifies the
> following (nearly) deterministic scheme.
>
> Beginning with the prose form of the name:
>
> 1. Convert the phrase to plain ASCII and remove any apostrophes. For example,
>    "Müller's algorithm" might become "Muellers algorithm".
> 2. Divide this result into words, splitting on spaces and any remaining
>    punctuation (typically hyphens).
>     - _Recommended:_ if any word already has a conventional camel-case
>       appearance in common usage, split this into its constituent parts (e.g.,
>       "AdWords" becomes "ad words"). Note that a word such as "iOS" is not
>       really in camel case per se; it defies any convention, so this
>       recommendation does not apply.
>
> 3. Now lowercase everything (including acronyms), then uppercase only the
>    first character of:
>     - ... each word, to yield upper camel case, or
>     - ... each word except the first, to yield lower camel case
> 4. Finally, join all the words into a single identifier.
>
> Note that the casing of the original words is almost entirely disregarded.
> Examples:
>
> | Prose form              | Correct                               | Incorrect         |
> |:------------------------|:--------------------------------------|:------------------|
> | "XML HTTP request"      | XmlHttpRequest                        | XMLHTTPRequest    |
> | "new customer ID"       | newCustomerId                         | newCustomerID     |
> | "inner stopwatch"       | innerStopwatch                        | innerStopWatch    |
> | "supports IPv6 on iOS?" | supportsIpv6OnIos                     | supportsIPv6OnIOS |
> | "YouTube importer"      | YouTubeImporter <br> YoutubeImporter* |                   |
>
> *Acceptable, but not recommended.
>
> > Note: Some words are ambiguously hyphenated in the English language:
> > for example "nonempty" and "non-empty" are both correct, so the method
> > names checkNonempty and checkNonEmpty are likewise both correct.
