## INSTALL ZSH
sudo apt install zsh fonts-font-awesome

# Install oh-my-zsh
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

# Enable Autosugestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting


# Edit plugins in .zshrc
plugins=(git zsh-autosuggestions)


## INSTALL KUBECTL
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl

# If the folder `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring

# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly

sudo apt-get update
sudo apt-get install -y kubectl

## UPDATE PYTHON PATH
sudo ln -s /usr/bin/python3 /usr/bin/python
sudo apt install python3-pip
sudo ln -s /usr/bin/pip3 /usr/bin/pip

## Kubectl Completion
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null

## INSTALL PODMAN and DOCKER COMPOSE
sudo apt install -y podman
sudo apt install -y podman-docker

sudo apt install podman-compose

sudo systemctl --user status podman.socket podman.service
sudo systemctl --user enable podman.socket
sudo systemctl --user start podman.socket
sudo systemctl --user status podman.socket podman.service

## INSTALL VSCODE THIS MAY NOT BE NEEDED ANYMORE
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg

sudo apt install apt-transport-https
sudo apt update
sudo apt install code

## INSTALL .NET
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-8.0

## INSTALL AZ CLI -- does not yet work for 24.04 will work on 5/21
sudo apt install azure-cli


# CHANGE DEFAULT EDITOR
sudo update-alternatives --config editor
