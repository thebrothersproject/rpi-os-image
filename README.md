# rpi-os-image
# Contains the Ubuntu Mate 18.04 image used to generate SD card 

# Instructions for cloning the repository:

1) If you have not already installed/configured git, do so now:

sudo apt-get install git
git --version
git config --global user.name "<your name>"
git config --global user.email "<your email>"

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

4) On Windows 10: Download tool called Etcher used to flash microSD card

Download https://www.balena.io/etcher/

4) With the microSD/USB adapter connected to your PC, launch Etcher flash the image onto the SD card.

# Here is a guide you can follow: https://linuxhint.com/install_ubuntu_mate_raspberry_pi/
# (we're using the 18.04 version of ubuntu instead of 16.04 in this guide, but it is pretty similar)

# As an FYI:
# The first time I tried this I had just re-formatted the SD card (not required for Etcher) and I selected the the .zip folder instead of the .iso file in Etcher. At the end, it said the flash failed (I think b/c of checksum error b/w src and dst). Trying again, I extracted the zip folder and selected the .iso and it worked fine. I read that Etcher should handle the .gz/.zip files just fine, so not sure if this step is needed or not.

5) Once the SD card has been created, insert into the raspberry pi, connect display, keyboard, mouse and power supply. It should boot as per the above guide.

6) Update and upgrade packages for security. We won't upgrade again after this in an attempt to not break dependencies.

sudo apt update
sudo apt upgrade

6) Set up ssh server so that you don't need to connect keyboard and display to work. You can ssh in through your laptop/VM.

# Install the ssh server
sudo apt install openssh-server
# Install sshguard for security
sudo apt install sshguard
# Enable the ssh server to start on boot up
sudo systemctl enable ssh 
# Start the ssh server
sudo systemctl start ssh
# Check to make sure that ssh is running
sudo systemctl status ssh
#(You should see Active: active (running) highlighted)

# Generate openssh keys (my keys were not automatically generated for some reason... look for /etc/ssh/ssh_host_dsa_key and corresponding .pub file)
sudo key-gen -A

#These commands are from here: https://ubuntu-mate.org/raspberry-pi/
#and here: https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/

7) Test the ssh connection from your VM/PC connected on wifi to the same network as raspberry pi

# There are a few ways to find IP address of the RPi:
# If you have access to a terminal on the rpi, you can run:
# "ifconfig | grep inet" or "ip a | grep inet" without the quotes.

# This will show you a few addresses, but you are interested in the address from the line also showing a broadcast address (ending in .255)

# If you're trying to ssh though and you don't know the ipaddress, the arp-scan utility will be helpful.

# Install with the following command
sudo apt install arp-scan
# Scan for ipaddresses connected to the network
sudo arp-scan -l
# The tricky part is sorting through all the ip addresses if you're on wifi with lots of connected devices. When I ran this, it showed the name of the device manufacturer after the address. So you could easily find the address with "sudo arp-scan -l | grep Raspberry" without the quotes.

# The ssh command is:

ssh username@ipaddress

# for me this was

ssh david@192.168.1.29

# if this fails, run "sudo systemctl status ssh" on the rpi again to see if there are any error messages.

### Congratulations, your Raspberry Pi is all set up. At this point we'll install Docker (see doc/Docker_installation.txt)

