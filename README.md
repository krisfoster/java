# GraalVM EE Docker Based Local Setup (with support for X11)

## Overview
This repo demonstrates how to have a repeatable GraalVM EE environment that
with support for local editing, from within VSCode

## Host Setup
Host here refers to your laptop.

### VSCODE
Install VSCode - you may ind you actually like it :)

The following extensions are required and should be installed:

* Remote Containers (Microsoft)
* Remote SSH (Microsoft) - not needed for this, but very useful
* Java Extension Pack (Microsoft)
* Project Manager for Java (Microsoft)

Can you also try out the GraalVM VSCode plugins....

### Windows
**TODO**

### Linux
**TODO**

### OSX
1. Install XQuartz. This is an X Windows server. It will run your X Windows system
2. Configure X windows

```sh
# I am not entirely sure if this is required, but what can it hurt :)
sudo defaults write org.x.X11 nolisten_tcp 0

# Allow connections from your local host, which will include the docker container
/usr/X11R6/bin/xhost +localhost
```
3. Start XQuartz

## Starting up Your DEV Container
* Click on the Remote Explorer Icon on the Left hand Ribbon
* Containers
** Click on the '+' > "Open Current Folder in COntainer"
** Wait... it will build your container
* Start your shell, (Terminal > New Terminal ) when the container has been built, You might need to select from the shell drop-down in the Terminal Window

## Rebuilding & Stopping the Container
You can rebuild the container at any time. If you started an X Server, ou can test
this out with the following, run form within the shell in VSCode.

```sh
# Enjoy all the XOrg goodness
$ xeyes
```