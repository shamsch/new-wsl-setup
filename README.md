## How I setup WSL Ubuntu for development
## Table of Contents
1. [Install WSL](#install-wsl)
2. [See user and OS details](#see-user-and-os-details)
3. [User setup](#user-setup)
4. [Install updates](#install-updates)

### Install WSL
1. [Enable WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
2. [Install Ubuntu from the Microsoft Store](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6)
3. [Install Windows Terminal from the Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)
### See user and OS details
1. See user
```bash
whoami
```
which should return
```bash
shamsur
```
or 
```bash
root
```
2. See all users
```bash
getent passwd
```
```bash
getent passwd | awk -F: '{ if ($3 >= 1000 && $3 != 65534) print $1 }' # Only show human users
```
3. See OS details
```bash
lsb_release -a
```

### User setup
1. Create a new user if not already created
```bash
sudo adduser shamsur
```
2. Add user to sudo group
```bash
sudo usermod -aG sudo shamsur
```
3. Switch to new user
```bash
su - shamsur
```
4. Confirm sudo access
```bash
sudo whoami
```
should return
```bash
root
```
5. See all sudo users
```bash
grep -Po '^sudo.+:\K.*$' /etc/group
```
6. Sudo without password
```bash
sudo visudo
```
and add the following line
```bash
shamsur ALL=(ALL) NOPASSWD: ALL
```
7. Remove a user from sudo group
```bash
sudo deluser shamsur sudo
```
8. Delete a user
```bash
sudo deluser shamsur
```

### Install updates
1. Update Ubuntu
```bash
sudo apt update && sudo apt upgrade
```
### Install ZSH
1. Install ZSH
```bash
sudo apt install zsh
```
2. Install Oh My ZSH
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
3. Set ZSH as default shell
```bash
chsh -s $(which zsh)
```
and set theme to agnoster (optional)
```bash
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="agnoster"/g' ~/.zshrc
```
make sure to have the terminal font set to MesloLGS Nerd Font in Windows Terminal settings
4. Restart shell
```bash
exec $SHELL
```
5. Confirm ZSH installation
```bash
zsh --version
```
### Install Brew
1. Install Brew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2. Add Brew to PATH
```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.zshrc
```
3. Restart shell
```bash
exec $SHELL
```
4. Confirm Brew installation
```bash
brew --version
```

### Install Git
1. Check Git exist
```bash
git --version
```
if not, install Git
```bash
sudo apt install git
```
2. Configure Git
```bash
git config --global user.name "Shamsur Raza Chowdhury"
git config --global user.email "shamsur314@gmail.com"
```
3. Confirm Git configuration
```bash
git config --list
```

### SSH setup for GitHub
1. Generate SSH key
```bash
ssh-keygen -t ed25519 -C "shamsur314@gmail.com"
```
and press enter to save the key in the default location
2. Add SSH key to ssh-agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```
3. Copy SSH key to clipboard
```bash
xclip -selection clipboard < ~/.ssh/id_ed25519.pub
```
Install xclip if not already installed
```bash
sudo apt install xclip
```
4. Add SSH key to GitHub
5. Test SSH connection
```bash
ssh -T
```


### Install Node.js with nvm
1. Install nvm
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
2. Add nvm to PATH
```bash
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.zshrc
```
3. Restart shell
```bash
exec $SHELL
```
4. Install Node.js
```bash
nvm install node
```
5. Set global Node.js version
```bash
nvm use node
```
6. Confirm Node.js version
```bash
node -v
```
```bash	
npm -v
```
### Install Yarn
1. Install Yarn
```bash
npm install --global yarn
```
### Install Docker
1. Install Docker
```bash
sudo apt install docker.io
```
2. Install Docker Compose
```bash
sudo apt install docker-compose
```
3. Add user to Docker group
```bash
sudo usermod -aG docker $USER
```
4. Restart shell
```bash
exec $SHELL
```
5. Confirm Docker installation
```bash
docker --version
```
```bash
docker-compose --version
```
### Install Python with pyenv
1. Install pyenv

```bash
sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev
```
```bash
curl https://pyenv.run | bash
```

2. Add pyenv init to shell
```bash
echo 'eval "$(pyenv init --path)"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```
3. Restart shell
```bash
exec $SHELL
```
4. Install Python
```bash
pyenv install 3.8.5
```
5. Set global Python version
```bash
pyenv global 3.8.5
```	
6. Confirm Python version
```bash
python -V
```
7. Change Python version
```bash
pyenv global 3.9.0
```
### Install Nano    
1. Install Nano if not already installed
```bash
sudo apt install nano
```
2. Set Nano as default editor
```bash
export EDITOR=nano
```
3. Check default editor
```bash
echo $EDITOR
```


### List your installed packages
1. List your installed packages
```bash
apt list --installed
```
2. Using Homebrew
```bash
brew list
```
### Uninstall packages
1. Uninstall package
```bash
sudo apt remove <package-name>
```
2. Uninstall using Homebrew
```bash
brew uninstall <package-name>
```

### Update all packages
1. Update all packages
```bash
sudo apt update && sudo apt upgrade
```
```bash	
brew update && brew upgrade
```	

---