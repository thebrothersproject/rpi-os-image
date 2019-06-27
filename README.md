# rpi-os-image
Contains the Ubuntu Mate 18.04 image used to generate SD card 

Instructions for cloning the repository:

1) If you have not already installed/configured git, do so now:

sudo apt-get install git
git --version
git config --global user.name "David Bumpus"
git config --global user.email "dbumpus@mail.bradley.edu"

2) Clone the repository

mkdir git
cd git/
git clone https://github.com/thebrothersproject/rpi-os-image.git
cd rpi-os-image/

3) Download the Raspberry Pi OS image for SD card creation

Download from the following page:
https://ubuntu-mate.org/download/

Choose the version recommended for Raspberry Pi (for aarch32 ARMv7 computers)
Like raspberry pi model 3 b, model 3 b+.
