# CoLRev development environment setup

This document describes the setup of a development environment for the CoLRev project.

The setup includes:
- Python3, pip
- git
- Docker
- CoLRev
- continuous integration (pre-commit hooks)
- VisualStudio

A fully installed VirtualBox image is available [here](https://gigamove.rwth-aachen.de/de/download/9453143c22408f2757dfd9946ec2fe0a). If the link has expired, please contact [Gerit Wagner](mailto:gerit.wagner@uni-bamberg.de).

The documentation can be used to set up the environment on other machines.
Although we only support the VirtualBox/Ubuntu setup, useful hints for the setup on other machines can be contributed to this repository (issues or pull-requests).

Before using the setup, please update your git credentials (using the shell):

```
git config --global user.name "Lisa Smith"
git config --global user.email "lisa.smith@stud.uni-bamberg.de"
git config --global credential.helper store
```

Create an SSH key pair and register the public key at Github ([steps](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)).


To activate copy-paste between the VM and your OS: Geräte &rarr; Gemeinsame Zwischenablage &rarr; bidirektional


To test colrev, open a Terminal (``Alt``+``Ctrl``+``T``), navigate to an empty directory, and run:

```
colrev init
```

Installation log:

- Image: [Ubuntu 22.04.2 LTS](https://ubuntu.com/download/desktop/thank-you?version=22.04.2&architecture=amd64)
- VirtualBox: [Version 7.0.6](https://www.virtualbox.org/) with Guest additions
- Account: 
  - Username: ubuntu
  - Password: ubuntu

```
sudo apt install python3-pip
sudo apt install git
sudo apt install gitk
sudp apt install python3-poetry
pip3 install poetry pytest-mock pylint pytest
sudo snap install --classic code

sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

python3 -m pip install --upgrade pip

cd ~/Desktop && git clone https://github.com/CoLRev-Ecosystem/colrev && cd colrev
pip3 install -e .

cd ~/Desktop
git clone https://github.com/geritwagner/dev-setup

```
