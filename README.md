ansible-pids
============

Simple ansible module for handling PIDs.

## Overview

This module reads a list of PID-files, concatenates the contents and saves the result in a fact. Null-strings in PID-files will be ignored.

## Example

```
ansible all -m pids -a "path=/usr/local/project/.pids/ pid_files='mon_1376871534954026565.pid mon_1376871534954026566.pid' register=var"
```
## Installation

Copy the module into your project's library directory.

```
cp -R library /your/project/library/
```
