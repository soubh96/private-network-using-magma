# AGW Deployment Guide

## Prerequisites

### 1.1 Install Python using pyenv

1. Update and upgrade system packages:
   ```bash
   cd && sudo apt update && sudo apt upgrade -y
   sudo apt install -y git fakeroot
2.Install pyenv:
cd && git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init --path)"' >> ~/.profile
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init --path)"\nfi' >> ~/.bashrc
source ~/.bashrc && source ~/.profile
exec "$SHELL"
3.Install required dependencies:
sudo apt-get update
sudo apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
nstall Python 3.7.3:

bash

pyenv install --list | grep " 3\.[678]"
pyenv install 3.7.3
pyenv global 3.7.3
python -V

Install basic Python packages:

bash

    cd && pip3 install ansible fabric3 jsonpickle requests PyYAML

1.2 Install VirtualBox and Vagrant

    Install VirtualBox:

    bash

sudo apt update && sudo apt -y upgrade
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
sudo apt update
sudo apt-get install -y virtualbox-6.1

