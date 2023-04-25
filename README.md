# CoLRev development environment setup

This document describes the setup of a development environment for the CoLRev project.

The setup includes:
- Python3, pip
- git
- Docker
- CoLRev
- continuous integration (pre-commit hooks)
- VisualStudio

A fully installed VirtualBox image is available [here](https://gigamove.rwth-aachen.de/de/download/29146e80c3ec3e691e35b4866e9573c9). If the link has expired, please contact [Gerit Wagner](mailto:gerit.wagner@uni-bamberg.de).

The documentation can be used to set up the environment on other machines.
Although we only support the VirtualBox/Ubuntu setup, useful hints for the setup on other machines can be contributed to this repository (issues or pull-requests).

After unpacking the VirtualBox Image, open the ``colrev_dev.vbox`` file in [VirtualBox](https://www.virtualbox.org/).
To avoid performance issues, the following settings are recommended:

```
Settings - system - acceleration
- KVM recommended for Linux guests
- Hyper-V recommended for WIndows guests
Settings - display - disable 3D acceleration
```

Start the machine, and log in (account: ``ubuntu``, password: ``ubuntu``).
Before using the setup, please update your git credentials (using the shell / ``ctrl+alt+t``) and pull the latest version of CoLRev:

```
git config --global user.name "Lisa Smith"
git config --global user.email "lisa.smith@stud.uni-bamberg.de"
git config --global credential.helper store
cd ~/Desktop/colrev
git pull
```

Create an SSH key pair and register the public key at Github ([steps](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)).

To activate copy-paste between the VM and your OS: Geräte &rarr; Gemeinsame Zwischenablage &rarr; bidirektional

To test colrev, open a Terminal (``Alt``+``Ctrl``+``T``), navigate to an empty directory, and run:

```
colrev init
```

## Installation log
- Image: [Ubuntu 22.04.2 LTS](https://ubuntu.com/download/desktop/thank-you?version=22.04.2&architecture=amd64)
- VirtualBox: [Version 7.0.6](https://www.virtualbox.org/) (no unattended installation)
- Account:
  - Username: ubuntu
  - Password: ubuntu

```
sudo apt-get install virtualbox-guest-additions-iso
sudo apt install git
sudo apt install gitk
sudo snap install --classic code
sudo apt install vim

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

sudo apt install python-is-python3
sudo apt install python3-pip
python3 -m pip install --upgrade pip
python3 -m pip install poetry pytest-mock pylint pytest pre-commit
python3 -m pip install --upgrade paramiko

cd ~/Desktop
git clone git@github.com:geritwagner/dev-setup.git
git clone git@github.com:CoLRev-Environment/colrev.git
cd colrev
pip3 install -e .
pre-commit install
pre-commit run --all
cd ~/Desktop
mkdir test
cd test
colrev init --example
# Complete run to pull the Docker images

```
