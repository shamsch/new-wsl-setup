## How I setup WSL Ubuntu for development
### Install WSL
1. [Enable WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
2. [Install Ubuntu from the Microsoft Store](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6)
3. [Install Windows Terminal from the Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)

### User setup
1. Create a new user
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
4. Confirm user change
```bash
whoami
```
5. Confirm sudo group membership
```bash
groups
```
6. Confirm sudo access
```bash
sudo whoami
```
7. Confirm sudo access without password
```bash
sudo -l
```
8. List users
```bash
cat /etc/passwd
```
9. Delete user
```bash
sudo userdel -r shamsur
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
3. Confirm installation
```bash
zsh --version
```
4. Set ZSH as default shell
```bash
chsh -s $(which zsh)
```
5. Restart shell
```bash
exec $SHELL
```
### Install Git
1. Install Git
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

### SSH setup
1. Generate SSH key
```bash
ssh-keygen -t rsa -b 4096 -C "
```
2. Add SSH key to ssh-agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
3. Copy SSH key to clipboard
```bash
clip < ~/.ssh/id_rsa.pub
```
4. Add SSH key to GitHub
5. Confirm SSH key
```bash
ssh -T
```
### Install Node.js with nvm
1. Install nvm
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
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
sudo npm install --global yarn
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
1. Install dependencies
```bash
sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev
```
2. Install pyenv
```bash
curl https://pyenv.run | bash
```
3. Add pyenv to PATH
```bash
echo 'export PATH="$HOME/.pyenv/bin:$PATH"' >> ~/.zshrc
```
4. Add pyenv init to shell
```bash
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```
5. Add pyenv virtualenv-init to shell
```bash
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
```
6. Restart shell
```bash
exec $SHELL
```
7. Install Python
```bash
pyenv install 3.8.5
```
8. Set global Python version
```bash
pyenv global 3.8.5
```
9. Confirm Python version
```bash
python -V
```
10. Change Python version
```bash
pyenv global 3.9.0
```
### Install Nano    
1. Install Nano
```bash
sudo apt install nano
```
### Install VS Code in WSL
1. Install VS Code
```bash
sudo apt install code
```
2. Install VS Code Remote Development extension

## Must know commands
### ZSH
- `zsh --version` - Confirm ZSH installation
- `chsh -s $(which zsh)` - Set ZSH as default shell
