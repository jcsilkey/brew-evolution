# Homebrew Configuration Files
## Introduction
I'd like the ability to store Homebrew settings in a configuration file

## Motivation
The motivation for this feature is to allow users to create systemwide and/or 
per-user files for configuring homebrew rather than setting environmental variables.
This would allow all users or system jobs to use the same settings while
maintaining the ability to override them on a per user basis.

## Proposed solution
When invoked, homebrew would search specific system locations for a configuration file
and load the file if found. It would also load an existing configuration file from
the user's home folder. Finally, users could continue to override settings using the
current environmental variable method.

Currently, the only way to set Homebrew options is via environmental variable. There is
no way to share settings between users or system jobs setting them individually.

## Detailed design
A prototype implementation can be found at
https://github.com/jcsilkey/microbrew/tree/feature/homebrew-config-file.

1. Upon execution, `brew` would search /etc/homebrew/homebrew.json and 
$HOMEBREW_PREFIX/etc/homebrew/homebrew.json for a configuration file and load the
first file found.
2. `brew` would then search for $HOME/.homebrew/homebrew.json and load it if found.
3. Any options previously set via environmental variables are ignored, allowing users
to continue setting options via the current process.
4. The configuration loader utilizes a whitelist to only load specific settings
from the configuration file.

## Alternatives considered
1. Adding environmental variables in /etc/profile or /etc/bashrc.
