# Version Control

All custom code that will be used in a production environment must be kept in a
version control system (VCS). The VCS must be used to track changes to the
codebase as it is growing and evolving.

## Commits

###### Commit and push frequently

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
properly, it can result in a cleaner commit history. For details, see the [Git
documentation](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_squashing).
Make sure to create a new commit message that fully and accurately captures the
nature of the change.

----

### Commit Messages

###### Use descriptive commit messages

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

_Example:_

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

GitHub hosts CyberScout's central repositories. The code hosted there is
considered the _canonical_ repository.

Any developer or other person that will be working with CyberScout's code must
have a GitHub account. The CyberScout GitHub administrator(s) will assign the
person to a team or add them as a collaborator. The administrator will need the
GitHub username or email address of the new team member or collaborator.

### Global Config

Each developer needs to have the following global configuration for their Git
installation.

###### `user.name`

Set this option to your real first and last name.

```bash
$ git config --global user.name 'Tasmanian Devil'
```

###### `user.email`

Set this option to the email address that is associated with your GitHub
account. CyberScout employees and contractors should use their '@cyberscout.com'
address.

```bash
$ git config --global user.email taz.devil@helpfulconsultants.com
```

###### `core.autocrlf`

This option controls how line endings are interpreted and saved in the code
base. Since CyberScout uses a mix of platforms for development, it is important
that this option is configured correctly. See the
[Git documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#__code_core_autocrlf_code)
for details.

**Windows** users must set this option to `true`:

```windows
C:\> git config --global core.autocrlf true
```

**macOS or Linux** users must set this option to `input`:

```bash
$ git config --global core.autocrlf input
```

###### `core.excludesfile`

This option will establish a default set of patterns that git will ignore. The
[global gitignore file](git-scm/cyberscout-global.gitignore) should be saved to
local storage, and then configured in Git.

```bash
$ git config --global core.excludesfile '/path/to/the/cyberscout-global.gitignore'
```

## Versioned Files

###### Ignore system-specific files

The default `.gitignore` file configured above will ignore most system-specific
files that we are likely to work with. However, other files, like Java
`.properties` files, might be generic or specific.

Therefore, care must be taken that no system-specific files are checked into
source control. Such files (or values) cause problems for other developers,
because the code will not compile and/or run on their machine without
modifications. Then, when they commit their code changes, the system-specific
files also get checked in, which clutters the commit history.

Most importantly, such files can represent a **security risk**, because
sensitive information, like user names and passwords, can become visible to
unauthorized persons.

The following is a partial list of items that **_must not_** be checked into
source control. _Ever_. Not even non-production values.

1. User names
2. Passwords
3. API keys
4. Private encryption keys
5. Encryption passphrases
6. Customer PII

The following is a partial list of items that _should not_ be checked into
source control without a very good reason. These values can cause problems for
others that work on the code base.

1. System names (simple or fully-qualified)
2. IP addresses
3. Absolute file system paths (i.e. `C:\Windows\System32\some.dll`)
4. System-specific file system paths (i.e. `path/to/your/working/dir`)

## Lines of Development

### Forks

### Branches

### Tags

### Releases

