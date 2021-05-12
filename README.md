# misc-updater

## <small>Check </small>M<small>anually-</small>I<small>nstalled and </small>S<small>ource-</small>C<small>ompiled (MISC) packages for updates.</small>

----

## Introduction

On Linux systems, one generally installs packages through their distribution's
dedicated package manager (e.g. `apt` on ubuntu-based systems).

However, for whatever reason, every now and then, one needs to install a package
on their systems manually, whether this comes in the form of a pre-packaged
tarball that simply needs to be extracted at an appropriate location, or a
source-tarball that needs to be compiled and installed via the usual
`./configure && make && make install` mechanism, etc.

One of the main functions of a package manager is to check whether newer
releases exist for the packages installed on the system, and notify the user
when such updates exist. However, in the case of MISC packages, unless a package
implements its own 'check for updates' mechanism, the user is not aware when
updates are released, unless they periodically remember to manually check the respective
websites of all MISC packages installed on the system.

This script is a super-simple approach to solving that problem.

----

## Usage

### The script:

This repository contains a simple example script which checks a selection of MISC packages, and notifies the user when a new version has been released for any of the packages defined inside. In my case, it checks for:

 - The amazing [Gnu Nano](https://nano-editor.org/) editor (latest source release) --- the version typically offered by most linux distros tends to be horribly outdated!
 - [Anki](https://apps.ankiweb.net/) (latest binary tarball) --- Anki sometimes notifies you of updates, but not always)
 - [Gnu Octave](https://www.gnu.org/software/octave/) (latest source release) --- the version typically offered by most linux distros tends to be horribly outdated, and generally compiling from source is much more versatile. The gui interface does actually notify you of new releases, but the cli (which I prefer to use) does not.
 - [Julia](https://julialang.org/) (latest binary tarball)
 - The [JabRef](https://www.jabref.org/) bibliography manager (latest .jar file)
 - The [Zoom Video Conferencing](https://zoom.us) application (latest .deb file)

Have a read, and adapt your script in a similar manner for your own packages. :)

### How to use:

I use this alongside my normal package manager's cli updater. E.g., I have `misc-updates` installed in my `/usr/local/bin`, and this line inside my `.bashrc`:

    alias checkupdates='mintupdate-cli -r list; echo; misc-updates'

## Notes

- The script is extremely simple and should be simple enough to follow and modify without much need for detailed explanation. The basic idea is that one identifies a website for each project that can be easily parsed to identify the latest release, and then compare it to a locally defined value.
  - In many cases, the best approach is to look for a fixed URL that always points to the 'latest release'. This is commonly provided in github-based releases, for instance.

- This script is intended to act as an 'updater', not an 'upgrader'.
    I.e. it is not intended to 'upgrade' packages, it simply checks for 'updates' and notifies the user to act accordingly if any exist (i.e. much like a normal package-manager's `update` function).

-   Once a the script has flagged an update, and the user has manually upgraded their packages, it is the user's responsibility to update the script's values to point to the new versions as appropriate.
