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
