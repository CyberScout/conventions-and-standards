# Version Control

All custom code that will be used in a production environment must be kept in a
version control system (VCS). The VCS must be used to track changes to the
codebase as it is growing and evolving.

## Commits

To ensure that work in progress is not lost, commits should be made frequently
&mdash; several times a day &mdash; and pushed up to the central repository at
least once a day. Commits should be made at some logical milestone, but not
necessarily when the change is "complete". The code doesn't even have to be
working when it's committed. For example, when implementing a new feature,
commits might be done after:

1. stubbing out the new methods
2. implementing a high-level flow in a public method
3. implementing each private method
4. writing each unit test for that public method
5. writing a unit test for one of the private methods, and changing its
   visibility to package-private
6. repeating for each new method needed

The commits can really be as granular as desired, as long as they are not being
made directly to an integration or production branch.

----

###### :information_source: Squashing Git Commits

Git allows individual commits to the "squashed" down into a single commit. This
can allow a developer to rewrite their tiny "work-in-progress" commits into one
or a few larger commits. These would capture the same changes, but with a
history that's easier to follow and with fewer commits that would be considered
broken.

:warning: _Use this feature with care._ Commit history cannot be changed once it
has been published (e.g. pushed to the central repository). However, if used
properly, it can result in a cleaner commit history. For details, see the [git
documentation](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_squashing).
Make sure to create a new commit message that fully and accurately captures the
nature of the change.

----

### Commit Messages

Commit messages must be descriptive, such that a reader of the commit log can
easily determine what logical changes are in a particular commit. Whenever
possible, they should also link to the issue tracking or project management
system where the bug or feature is documented.

A good commit message will contain the issue link and a very brief summary in
the first line. Subsequent lines will add details about the commit itself,
including the root cause of the bug, how it was fixed, and why the particular
solution was chosen.

The commit message must _not_ consist solely of the issue link, because a commit
log reader can't determine what's in the commit without consulting another
system.

###### Example

```
BUG-2345: Fixed duplicate 'Create Customer' transactions

The application was creating multiple 'Create Customer' transactions during a
single request because of some faulty logic inside a while-loop.

Changed the condition for breaking out of the loop so that only the first
matching element causes the customer to be created.
```

## Git

Our VCS of choice is currently Git. All custom code must be checked into a Git
repository.

### GitHub

### Global Config

## Ignore Configuration Files

### No Passwords

## Line endings

## Branches, Tags, and Releases
