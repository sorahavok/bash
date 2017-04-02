# Setup
Run this to set up all my defaults:

   cd ~
   mkdir ~/GitHub
   git clone https://github.com/sorahavok/bash.git ~/GitHub/bash
   sudo chmod +x ~/GitHub/bash/personal-setup.sh
   sudo ~/GitHub/bash/personal-setup.sh

## Personal Setup (Current Content)
```bash
#!/bin/sh
DB_TYPE=false
GRPC_TYPE=false
while getopts ":dg" opt; do
    case $opt in
        d)
            DB_TYPE=true
            echo "-d was triggered!" >&2
            ;;
        g)
            GRPC_TYPE=true
            echo "-g was triggered!" >&2
            ;;
        \?)
            echo "Invalid option: -$OPTARG" >&2
            ;;
    esac
done
echo "Flags:DB_TYPE(-d)=$DB_TYPE,GRPC_TYPE(-g)=$GRPC_TYPE"

# Install the basics
sudo apt install git vim python3-pip
pip3 install --upgrade pip

# Get some random python libs TODO: put these behind flags
pip3 install urllib3
pip3 install plotly

# Get an awesome .vimrc from GitHub
if [ -f /root/.vim_runtime ]; then
    git clone https://github.com/amix/vimrc.git ~/.vim_runtime
    sh ~/.vim_runtime/install_awesome_vimrc.sh
fi

# Install mongo and set up database folder if -d flag is set
if $DB_TYPE; then
    echo "Setting up DB" >&2
    pip3 install pymongo
    sudo apt install mongodb
    sudo mkdir /data/db
    sudo chown $USER -R /data/
fi

# Grab gRPC for protobufs and servers if -g flag is set
if $GRPC_TYPE; then
    echo "Setting up gRpC" >&2
    sudo pip3 install grpcio
    sudo pip3 install grpcio-tools
fi

## install zsh and replace bash with it
if [ ! -f /bin/zsh ]; then
    echo "Didn't find /bin/zsh, Installing it now" >&2
    sudo apt install zsh
    chsh -s `which zsh` # Change shell to wherever zsh was put
    cp ~/GitHub/bash/.zsh* ~/ # moving .zshrc and alias 
    echo "Exiting old shell, up arrow will not work because history is reset"
    exec zsh -l # Kill current process and start zsh (Thanks http://unix.stackexchange.com/questions/22721/completely-restart-bash)
fi
```
