# Setup
 Run this to set up all my defaults:
 
    cd ~
    mkdir ~/GitHub
    git clone https://github.com/sorahavok/bash.git ~/GitHub/bash
    sudo chmod +x ~/GitHub/bash/personal-setup.sh
    sudo ~/GitHub/bash/personal-setup.sh

## Personal Setup (Current Content)
```python
sudo apt install git
sudo apt install vim

## install zsh and replace bash with it
sudo apt install zsh
chsh -s `which zsh` # Change shell to wherever zsh was put
exec zsh -l # Kill current process and start zsh (Thanks http://unix.stackexchange.com/questions/22721/completely-restart-bash)


# Get an awesome .vimrc from GitHub
git clone https://github.com/amix/vimrc.git ~/.vim_runtime
sh ~/.vim_runtime/install_awesome_vimrc.sh

# Install mongo and set up database folder
sudo apt install mongodb
sudo mkdir /data/db
sudo chown $USER -R /data/

# Install python3 pip if it is missing
sudo apt install python3-pip
pip3 install --upgrade pip

# Grab gRPC for protobufs and servers
sudo pip3 install grpcio
sudo pip3 install grpcio-tools

# Get required python libs
pip3 install pymongo
pip3 install urllib3
pip3 install plotly
```
