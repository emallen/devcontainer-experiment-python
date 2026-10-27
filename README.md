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

- Badge in lower left of VSCode says "Dev Container: Python 3 @ desktop-linux"
- Explorer has "\[Dev Container: Python 3 @ desktop-linux\]" appended after
  the folder name.
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
     - EditorConfig
     - ESLint
     - markdownlint
     - Pylance
     - Python
     - Python Debugger
     - Python Environments

  3. Recommended

     This is less predictable. It is going to vary based on what VSCode thinks
     at the time you look.
- If you open a Terminal in VSCode and do `touch example.dat`, the file will
  also become visible on your windows filesystem.

This is what I'm doing.

The advantage is you can see your files with File Explorer and also other
tools you have locally. It also saves on keeping multiple redundant copies.

The biggest drawbacks are

1. Needing to make sure line terminators don't get messed up. I've addressed
   that with a `.gitattributes` file that _should_ help.
2. Performance of filesystem operations from inside the container is less good
   than with volume options. Might not matter on some things. For things like
   doing a package manager install in the shared source tree, this can be big.
   There is an article in the VSCode documentation on having a volume mounted
   to a subfolder of the share to game that performance:
   <https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_use-a-targeted-named-volume>.
   While it talks about Node, I'm not sure to what degree similar applies in
   Python.

### Windows Copy with independent container copy

1. Open VSCode to the folder you cloned the repo.
2. When the toast notification pops up to tell you about devcontainers, select
   the option to clone in volume.

There might be another way to do this, but I struggle to find the command
sequence.

This will look very similar to the previous. Really, two things will
distinguish it:

- If you open a Terminal in VSCode and do `touch proof-of-isolation.dat`, the
  fill will **not** become visible on your windows filesystem.
- In **Remote Explorer** on the left side, the node for
  **Devcontainer-Experiment-Python** will show two Volume mounts, contrast the
  above that shows _one_ Volume mount and one _bind_ mount.

### Container copy only

1. Open VSCode.
2. **Command Pallette → Dev Containers: Clone Repository in Container Volume**
   and provide the GitHub Clone URL.

This will be very hard to distinguish from the independent copies version
above.

There are variations on this like using a Named Container Volume. I haven't
experimented with them.

### Missing something

If you are missing someting, in particular an extension not present in the
initial release of the Dev Container, use
**Command Pallette → Dev Containers: Rebuild Container**.
Note that the `F1` key will put focus into the Quick Access box that is
several tools, including the **Command Pallette** and prefix
with <!-- markdownlint-disable-next-line MD038  -->
 `> ` (a greater-than sign followed by a space) which makes the shared box
behave in **Command Pallette** mode rather than the default mode.

## Benefits

Regardless of which of the big three options you do with your source location
you should be able to see that a terminal `python --version` succeeds and
reports `Python 3.14.8` (or possibly a higher 3.14 version, if you are reading
this in the future). The `.devcontainer/devcontainer.json` picked a container
image tag that does have its publisher update it for updates to the third
component of the Python version, so, in theory, if the day after I commit
this, Python 3.14.9 releases and the DevContainer equivalent to Docker Hub
updates to use it, you might see `Python 3.14.9` instead. The alternative would
have been pinning the hash
 (`sha256:28835c112fd097cb6d2fe1e195b660d66ae051859070a9b871fa2308f35897d3`)
 rather than the tag (`3-3.14-trixie`). There are trade-offs to both routes.
 I've seen some indications that Depandabot can help with this if one goes the
 hash route.

## Running the app

 From a terminal inside the development container:
 `python ./my_amazing_app.py`
