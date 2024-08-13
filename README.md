
---

# AGW Deployment Guide

## Prerequisites

### 1.1 Install Python using pyenv

1. Update and upgrade system packages:
   ```bash
   cd && sudo apt update && sudo apt upgrade -y
   sudo apt install -y git fakeroot
   ```

2. Install `pyenv`:
   ```bash
   cd && git clone https://github.com/pyenv/pyenv.git ~/.pyenv
   echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
   echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
   echo 'eval "$(pyenv init --path)"' >> ~/.profile
   echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init --path)"\nfi' >> ~/.bashrc
   source ~/.bashrc && source ~/.profile
   exec "$SHELL"
   ```

3. Install required dependencies:
   ```bash
   sudo apt-get update
   sudo apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
   ```

4. Install Python 3.7.3:
   ```bash
   pyenv install --list | grep " 3\.[678]"
   pyenv install 3.7.3
   pyenv global 3.7.3
   python -V
   ```

5. Install basic Python packages:
   ```bash
   cd && pip3 install ansible fabric3 jsonpickle requests PyYAML
   ```

### 1.2 Install VirtualBox and Vagrant

1. Install VirtualBox:
   ```bash
   sudo apt update && sudo apt -y upgrade
   wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
   wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
   echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
   sudo apt update
   sudo apt-get install -y virtualbox-6.1
   ```

2. Install Vagrant:
   ```bash
   cd && wget https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_x86_64.deb
   sudo dpkg -i vagrant_2.2.16_x86_64.deb
   vagrant --version
   vagrant plugin install vagrant-vbguest
   ```

### 1.3 Install Docker

1. Install Docker essentials:
   ```bash
   sudo apt-get remove docker docker-engine docker.io containerd runc
   sudo apt-get update
   sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common net-tools
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   sudo apt-get install -y docker-ce docker-ce-cli containerd.io
   ```

2. (Optional) Use Docker as a non-root user:
   ```bash
   sudo groupadd docker
   sudo usermod -aG docker $USER
   ```

3. Verify Docker installation:
   ```bash
   docker run hello-world
   ```

4. Install Docker Compose:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
   docker-compose --version
   ```

## AGW Deployment Using Vagrant

### Environment Variables

Set the following environment variables:
```bash
export MAGMA_ROOT=~/magma-packages
export MAGMA_TAG=master
```

### Install Test AGW using Vagrant

1. Clone the Magma repository and check out the desired branch:
   ```bash
   cd && git clone https://github.com/magma/magma.git $MAGMA_ROOT
   cd $MAGMA_ROOT
   git checkout $MAGMA_TAG
   git branch  # To validate
   #   master
   # * v1.6
   ```

2. Deploy using Vagrant:
   ```bash
   cd $MAGMA_ROOT/lte/gateway/
   sudo su
   # Ensure you are in $MAGMA_ROOT/lte/gateway/ folder
   vagrant up magma --provision
   ```

3. Connect to the AGW:
   ```bash
   cd $MAGMA_ROOT/lte/gateway/
   sudo su
   vagrant ssh magma
   ```

At this point, you should be connected to the AGW and see something like `vagrant@magma-dev:~$` in the CLI.

---

Feel free to adjust the version numbers or commands according to your specific requirements.

