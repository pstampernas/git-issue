# Git Issues

This is a minimalist distributed issue management system based on Git.
It has the following advantages over other systems.

* **No backend**
  You can install and use _gi_ with a single shell script.
  There's no need for a server or a database back-end, and the corresponding
  problems and requirements for their administration.
* **Distributed asynchronous management**
  Anyone can add, comment, and edit issues without requiring online access
  to a centralized server.
  There's no need for online connectivity; you can pull and push issues
  when you're online.
* **Transparent text file format**
  Issues are stored as simple text files, which you can view, edit, share, and
  backup with any tool you like.
  There's no risk of loosing access to your issues because a server has
  failed.
* **Git based**
  Issues are changed and shared through Git.
  This provides _gi_ with a robust, efficient, portable, and widely available
  infrastructure.
  It allows you to reuse your Git credentials and infrastructure and also
  provides a solid audit trail regarding any changes.
  You can even use Git and command-line tools directly to make sophisticated
  changes to your issue database.

## Installation
Simply copy the `gi` shell script somewhere in the system's path.
If you have administrative access you can install it with
`sudo install gi /usr/local/bin`.
For your personal use,
assuming that the directory `~/bin` exists and is in your path,
you can install it with `install gi ~/bin`.
You can even put `gi` in your project's current directory and run it from there.

## Use
You use _gi_ with the following sub-commands.

* `gi init`: Verifies system functionality
  and creates a new issues repository in the current directory.
* `gi new`: Creates a new issue and marks it as open.
* `gi list`: Lists the issues with the specified tag.
  By default this lists issues that are tagged as `open`.
* `gi show`: Shows specified issue.
* `gi comment`: Adds an issue comment.
* `gi tag`: Adds (or removes with `-r`) a tag.
* `gi assign`: Assigns (or reassigns) an issue to a person.
  The person is specified with his/her email address.
  The form `@name` or `name@` can be used as a shortcut, provided it
  uniquely identifies an existing assignee or committer.
* `gi attach`: Attaches (or removes with `-r`) a file to an issue.
* `gi watch`: Adds (or removes with `-r`) an issue watcher.
* `gi close`: Removes the `open` tag from the issue, marking it as closed.

Issues and comments are specified through the SHA hash associated with the
commit that opened them.

## Internals
* All data are stored under `.issues`.
* A `.git` directory contains the Git data associated with the issues.
* An `issues` directory contains the individual issues.
* Each issue is stored in a directory named `issues/xx/xxxxxxx...`,
  where the x's are the SHA of the issue's initial commit.
* Each issue can have the following elements in its directory.
  * A `comments` directory where comments are stored.
  * An `attachments` directory where issue's attachments are stored.
  * A `tags` file containing the issue's tags, one in each line.
  * A `watchers` file containing the emails of persons to be notified when the issue changes (one per line).
  * An `assignee` file containing the email for the person assigned to the issue.