# MDRS Workspace (Kasm Image)

![Screenshot from 2023-06-09 09-48-15](https://github.com/capsulecorplab/mdrs-workspace-image/assets/14095576/0f7832dd-5ae3-4dba-8250-717fce19c81f)

## Introduction

This repo provides an Immutable-Infrastructure-as-Code (IIaC) workspace for the Mars Desert Research Station (MDRS), based on an Ansible template for [KASM Ubuntu Jammy](https://hub.docker.com/r/kasmweb/core-ubuntu-jammy) images.  The workspace is configured with the following software:

- git cli
- [Keychain](https://www.funtoo.org/Keychain)
- Firefox
- Python 3.8.x (part of the image template) with the following packages (not part of the image template)
    - pip
    - [JupyterLab](https://jupyter.org/)
    - [Jupyter Notebook](https://jupyter.org/)
    - [Voilà](https://voila.readthedocs.io/en/stable/index.html)
    - [Pint](https://pint.readthedocs.io/en/stable/)
- [QOwnNotes](https://www.qownnotes.org/) 23.12.5 (built from source)
- VS Code with the following extensions (note, auto-updates are disabled)
    - [Python extension by Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
    - [Dendron](https://marketplace.visualstudio.com/items?itemName=dendron.dendron)
    - [Foam](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode)
    - [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
- Artifact Generators
    - [PlantUML](https://plantuml.com/)
        - JDK v11
        - Graphviz 2.50 (built from source)
    - [AsciiDoctor](https://asciidoctor.org/) v2.0.17 with PlantUML and PDF support
- Open Source Hardware tools
    - [PrusaSlicer](https://github.com/prusa3d/PrusaSlicer) 2.7.0
    - [OpenSCAD](https://openscad.org/) 2021.01

## Requirements

1. A Bash terminal ([Ubuntu on WSL2](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#2-install-wsl) recommended for Windows users).
2. [Docker Compose](https://docs.docker.com/compose/install/) ([Docker Desktop](https://docs.docker.com/desktop/) recommended for non-Linux users)

## Setup/Installation

0. Install prerequisites 

As stated in the Requirements, installation requires a Bash terminal.  On Linux bash is readily available and on Mac the built-in terminal is sufficiently compatible.  On Windows we recommend a using a Linux virtual machine, which will include a real bash terminal, rather than a Linux-like environment such as Cygwin.  We recommend using the Windows Subsystem for Linux (WSL) as an easy and minimal way to run a Linux VM.  See the link in the Requirements section for instructions on how to install and configure Ubuntu on WSL.

Also as stated in the Requirements, installation requires Docker Compose, and the simplest way for non-Linux users to get that is via  Docker Desktop.  See the link in the Requirements section for instructions on how to install Docker Desktop.

Note: you should have Docker Desktop both installed _and running_ before running any docker-compose commands below.

From a bash terminal,

1. Clone this repo

```bash
cd ~
git clone https://github.com/capsulecorplab/mdrs-workspace-image.git
```
For those unfamiliar, this command will make a local copy of the mdrs-workspace-image repository into the current directory, using the Git source control system.  This step only needs to be done once.

2. Change directory into `mdrs-workspace-image`.

```bash
cd mdrs-workspace-image
```

3. Run `docker-compose pull` (Note: Linux users may need to prepend this command with `sudo`, and Windows and Mac users must have Docker Desktop running) to pull the published version of the workspace image or run `docker-compose build` to build the image locally.  This command is needed initially and can also be used later to retrieve updated versions of the repo.

## Using the image locally

Once pulled or built, the image can be run locally on port 6901 using docker-compose.

- **Starting the image locally:** Run `docker-compose up`
- **Stopping the image locally:** Use keyboard shortcut **Ctrl+C**

This starts up a Linux container (essentially a lightweight virtual machine) that is pre-configured with various tools needed for use at MDRS.  This virtual machine does not have its own window, instead it serves the desktop up over http/https.

When running locally, the workspace can be accessed at https://localhost:6901 with
- **User:** `kasm_user`
- **Passwordd:** `password`
