ansible-pids
============

Simple ansible module for handling PIDs.

## Overview

Actually, this module offers nothing specifically for working with PID-files. It reads a list of files, concatenates the contents and saves the result in a fact. Null-strings in files will be ignored. The name originates from the use case, to save all the PIDs from a list of PID-files in a fact, even when the PID-files contain Null-strings.

```
    - name: Retrieve PID-files
      command: /bin/ls {{ project_dir }}/.pids/
      register: uids
      ignore_errors: yes
    - name: Retrieve PIDs
      pids: path={{ project_dir }}/.pids/ pid_files="${uids.stdout}" register="pids"
      register: retrieve_pids
      ignore_errors: yes
      when: uids|success
    - name: Kill processes
      command: /bin/kill -s SIGTERM {{pids}}
      ignore_errors: yes
      when: uids|success and retrieve_pids|success
```


## Example

```
ansible all -m pids -a "path=/usr/local/project/.pids/ pid_files='mon_1376871534954026565.pid mon_1376871534954026566.pid' register=var"
```
## Installation

Copy the module into your project's library directory.

```
cp -R library /your/project/library/
```
