# devcontainer-experiment-python

Repo to hold my experiment in getting into development containers using Python
as my language of choice.

## Why

I'm working on learning Dev Containers, and decided to make my own repo to try
it out.

## Whom

Myself and a few collaborators with whom I'm discussing this journey.

## How

1. Have a tool that supports Dev Containers. I myself am using [VSCode](
    https://code.visualstudio.com/) with the **Dev Containers** extension (
    [`ms-vscode-remote.remote-containers`](
    https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)).

    As of this writing (October 2026), Dev Containers and VSCode support
    Linux Containers and not Windows Containers.

    My machine I'm using is Windows. My guidance will focus on having VSCode
    installed natively on Windows in a lightweight configuration, with the
    **Dev Containers extension** on the host (and anything that the mechanisms
    bring hostward), and most extensions operating _inside_ the container.

2. Decide where you want the source cloned.

   It is possible to either clone the source code from GitHub onto your Windows
   Filesystem and go from there, or to clone directly into a Docker Volume.

   If you clone it to your Windows host filesystem, you have a second choice:
   do you want to share the code on your host filesystem with the running
   devcontainer, or have a second copy for the devcontainer. There are pros
   and cons to each.

### Windows Shared with Container

   To have one copy stored on Windows but shared with the DevContainer

   1. Open VSCode to the folder you cloned the repo.
   2. **Command Pallette → Dev Containers: Reopen in Container**.

   If succcessful you should be able to tell by a few signs.

   - Badge in lower left of VSCode says "Dev Container: Python 3 @
     desktop-linux"
   - Explorer has "\[Dev Container: Python 3 @ desktop-linux\]" appended
     after the folder name.
   - Extensions shows \[at least\] three sections:
     1. Local - Installed

       This section will vary but will probably have at least:
       - Dev Containers

       One thing I like about this is that I won't have Extension Bloat
       where an extension I needed for one repo for 2 days bloats my machine
       forever. Such things will be in the second section.
     2. Dev Container: Python 3 @ desktop-linux - Installed

        This section should include:
        - autopep8
        - ESLint
        - Pylance
        - Python
        - Python Debugger
        - Python Environments
     3. Recommended

        This is less predictable.
