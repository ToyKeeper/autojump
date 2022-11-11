NAME
----

autojump - a faster way to navigate your filesystem

(ToyKeeper's lightly modded version, details below)

DESCRIPTION
-----------

autojump is a faster way to navigate your filesystem. It works by
maintaining a database of the directories you use the most from the
command line.

*Directories must be visited first before they can be jumped to.*

The original author (wting) seems to have abandoned autojump sometime in 2018,
so this is ToyKeeper's lightly modified version.  Changes are summarized in a
later section of this readme.

USAGE
-----

`j` is a convenience wrapper function around `autojump`. Any option that
can be used with `autojump` can be used with `j` and vice versa.

-   Jump To A Directory That Contains `foo`:

        j foo

-   Jump To A Child Directory:

    Sometimes it's convenient to jump to a child directory
    (sub-directory of current directory) rather than typing out the
    full name.

        jc bar

-   Open File Manager To Directories (instead of jumping):

    Instead of jumping to a directory, you can open a file explorer
    window (Mac Finder, Windows Explorer, GNOME Nautilus, etc.) to the
    directory instead.

        jo music

    Opening a file manager to a child directory is also supported:

        jco images

-   Using Multiple Arguments:

    Let's assume the following database:

        30   /home/user/mail/inbox
        10   /home/user/work/inbox

    `j in` would jump into /home/user/mail/inbox as the higher
    weighted entry. However you can pass multiple arguments to autojump
    to prefer a different entry. In the above example, `j w in` would
    then change directory to /home/user/work/inbox.

For more options refer to help:

    autojump --help

INSTALLATION
------------

### REQUIREMENTS

-   Python v2.6+ or Python v3.3+
-   Supported shells
    -   bash - first class support
    -   zsh - first class support
    -   fish - community supported
    -   tcsh - community supported
    -   clink - community supported
-   Supported platforms
    -   Linux - first class support
    -   OS X - first class support
    -   Windows - community supported
    -   BSD - community supported
-   Supported installation methods
    -   source code - first class support
    -   Debian and derivatives - first class support
    -   ArchLinux / Gentoo / openSUSE / RedHat and derivatives -
        community supported
    -   Homebrew / MacPorts - community supported

Due to limited time and resources, only "first class support" items will
be maintained by the primary committers. All "community supported" items
will be updated based on pull requests submitted by the general public.

Please continue opening issues and providing feedback for community
supported items since consolidating information helps other users
troubleshoot and submit enhancements and fixes.

### MANUAL

Grab a copy of autojump:

    git clone git://github.com/wting/autojump.git

Run the installation script and follow on screen instructions.

    cd autojump
    ./install.py or ./uninstall.py

### AUTOMATIC

#### Linux

autojump is included in the following distro repositories, please use
relevant package management utilities to install (e.g. apt-get, yum,
pacman, etc):

-   Debian, Ubuntu, Linux Mint

    All Debian-derived distros require manual activation for policy
    reasons, please see `/usr/share/doc/autojump/README.Debian`.

-   RedHat, Fedora, CentOS

    Install `autojump-zsh` for zsh, `autojump-fish` for fish, etc.

-   ArchLinux
-   Gentoo
-   Frugalware
-   Slackware

#### OS X

Homebrew is the recommended installation method for Mac OS X:

    brew install autojump

MacPorts is also available:

    port install autojump

Windows
-------

Windows support is enabled by [clink](https://mridgers.github.io/clink/)
which should be installed prior to installing autojump.

KNOWN ISSUES
------------

-   autojump does not support directories that begin with `-`.

-   For bash users, autojump keeps track of directories by modifying
    `$PROMPT_COMMAND`. Do not overwrite `$PROMPT_COMMAND`:

        export PROMPT_COMMAND="history -a"

    Instead append to the end of the existing \$PROMPT\_COMMAND:

        export PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND ;} history -a"

REPORTING BUGS
--------------

For any questions or issues please visit:

    https://github.com/wting/autojump/issues
    (or not ... wting abandoned the project in 2018)

CHANGES FROM UPSTREAM
---------------------

Compared to wting's last version (from 2018), a few things have been changed:

* Made scores/weights decay over time so more recently-used paths match first.
  Now if you used a directory once 5 years ago, it won't compete with a
  similarly-named path you used 5 minutes ago.  But an old dir you used many
  times will still beat a new dir you've only used once.
* No longer jumps to fuzzy matches when an exact match exists.  Fuzzy matches
  are disabled entirely, because they go to strange and unpredictable places.
* Match uncommon mid-path strings more easily.  Very handy when you have
  `/foo/bar/baz/devbranch/my/user/` and `/foo/bar/baz/stable/my/user/` and want
  to jump between the two `my/user/` directories with `j dev` and `j stab`.
* Prioritizes longer paths when there's a tie, because short paths don't need
  shortcuts as much.
* Uses python3 by default.  Python2 was replaced in 2008 and discontinued in
  2020.
* Fixed bug: Would fail to find current path in database when path contained a
  symlink.

AUTHORS
-------

autojump was originally written by Joël Schaerer, and currently
maintained by William Ting. More contributors can be found in `AUTHORS`.

COPYRIGHT
---------

Copyright © 2016 Free Software Foundation, Inc. License GPLv3+: GNU GPL
version 3 or later <http://gnu.org/licenses/gpl.html>. This is free
software: you are free to change and redistribute it. There is NO
WARRANTY, to the extent permitted by law.
