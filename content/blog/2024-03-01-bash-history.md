---
title: Better bash history
tags: bash config
---


Bash records your history as it goes but if you are operating across multiple windows it doesn’t work the way you would hope for - e.g. it is only recorded from a single given session, even if you work in multiple. PROMPT_COMMAND is a bash variable that is run as part of running commands. This particular one is designed to time and date stamp commands (not run as root) and their working directory into a daily log file. The logs live in ~/.logs/ so this needs to be made for the command to run mkdir -p ~/.logs.

export PROMPT_COMMAND='if [ "$(id -u)" -ne 0 ]; then echo "$(date "+%Y-%m-%d.%H:%M:%S") $(pwd) $(history 1)" >> ~/.logs/bash-history-$(date "+%Y-%m-%d").log; fi'
If I want to search my logs I can use grep <command> ~/.logs/* and it will tell me all the times and directories I ran a command, and how I ran it. The history in these log files is made up of all commands you run on the computer, regardless of how many terminal windows you have open.
