# CoLRev development environment setup

This document describes the setup of a development environment for the CoLRev project.

The setup includes:
- Python3, pip
- git
- Docker
- CoLRev
- continuous integration (pre-commit hooks)
- VisualStudio

A fully installed VirtualBox Image is available [here](https://gigamove.rwth-aachen.de/de/download/e03393275121c3e8d7d0775437b434a0). If the link has expired, please contact Gerit Wagner.

Before using the setup, please update your git credentials (using the shell):

```
git config --global user.name "Lisa Smith"
git config --global user.email "lisa.smith@uni-bamberg.de"
```

A fully configured Ubuntu/VirtualBox image is available [here](TODO).
The documentation can be used to set up the environment on other machines.
Although we only support the VirtualBox/Ubuntu setup, useful hints for the setup on other machines can be contributed to this repository (issues or pull-requests).

Installation log:

- Image: [Ubuntu 22.04.2 LTS](https://ubuntu.com/download/desktop/thank-you?version=22.04.2&architecture=amd64)
- VirtualBox: [Version 7.0.6](https://www.virtualbox.org/) with Guest additions
- Account: username:ubuntu, password:ubuntu

```
sudo apt install python3-pip
sudo apt install git
sudo apt install gitk
sudp apt install python3-poetry
pip3 install poetry pytest-mock pylint pytest
sudo snap install --classic code
sudo snap install docker.io
sudo gpasswd -a $USER docker
newgrp docker
python3 -m pip install --upgrade pip

cd ~/Desktop && git clone https://github.com/CoLRev-Ecosystem/colrev && cd colrev
pip3 install -e .

```