# Task.1-ROS
1. Set Locale
bash
نسخ الكود
#!/bin/bash

# Update package list and install locales package
sudo apt update && sudo apt install -y locales

# Generate and set locale to en_US.UTF-8
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

# Export the locale environment variable
export LANG=en_US.UTF-8

# Verify locale settings
locale
2. Setup Sources
a. Enable the Universe Repository
bash
نسخ الكود
#!/bin/bash

# Check if universe repository is enabled
if ! apt-cache policy | grep -q "universe"; then
    echo "Enabling Universe repository..."
    sudo apt install -y software-properties-common
    sudo add-apt-repository universe
fi

# Verify the universe repository is enabled
apt-cache policy | grep universe
b. Add the ROS 2 Apt Repository
bash
نسخ الكود
#!/bin/bash

# Update package list and install curl, gnupg2, lsb-release
sudo apt update && sudo apt install -y curl gnupg2 lsb-release

# Add ROS 2 GPG key
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

# Add the ROS 2 repository to the sources list
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# Update package list
sudo apt update
3. Install ROS 2 Packages
a. Upgrade System Packages
bash
نسخ الكود
#!/bin/bash

# Ensure the system is up to date
sudo apt upgrade -y
b. Install ROS 2 Desktop
bash
نسخ الكود
#!/bin/bash

# Install ROS 2 Foxy desktop version
sudo apt install -y ros-foxy-desktop
4. Environment Setup
a. Source the ROS 2 Setup Script
bash
نسخ الكود
#!/bin/bash

# Source the ROS 2 setup script
echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
source ~/.bashrc
Usage
Save each of the code blocks to separate shell script files, for example:

set_locale.sh
setup_sources.sh
install_ros2.sh
environment_setup.sh
Make the scripts executable:

bash
نسخ الكود
chmod +x set_locale.sh setup_sources.sh install_ros2.sh environment_setup.sh
Run the scripts in order:
bash
نسخ الكود
./set_locale.sh
./setup_sources.sh
./install_ros2.sh
./environment_setup.sh
This method ensures each step is clearly defined and executed in sequence, with additional checks and confirmations along the way.
