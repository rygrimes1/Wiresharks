#  SECTION 1: Initial System Setup, Repository Management, and Git Configuration 

## Initial system package update and GPG key fix (troubleshooting common Kali issues)
### This command updates the list of available packages.
sudo apt-get update --allow-releaseinfo-change

## This command adds the Kali Linux public key. This was needed because apt reported missing public keys for signature verification.
### Note: apt-key is deprecated, but used here as it was suggested by the system error.
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys ED65462EC8D5E4C5

## Find and disable the problematic Metasploit repository.
### This command searches for "metasploit" in apt's source lists to identify the file causing errors.
grep -r "metasploit" /etc/apt/sources.list /etc/apt/sources.list.d/
## After finding the file (e.g., /etc/apt/sources.list.d/metasploit-framework.list),the 'nano' text editor is used to open it and comment out the Metasploit line by adding '#' at the start.
sudo nano /etc/apt/sources.list.d/metasploit-framework.list

## Re-run system update after fixing repositories to confirm clean update.
sudo apt update --allow-releaseinfo-change
## Upgrade all installed packages to their newest versions.
sudo apt-get full-upgrade -y
## Reboot the system to apply major updates.
sudo reboot


## Navigate to your Wiresharks repository.
### This assumes your Wiresharks project is located in your home directory.
cd ~/Wiresharks

## Clone the bftdetector project into the current directory.
### This creates a 'bftdetector' folder inside '~/Wiresharks'.
### If you already ran this, it will show an error about the directory existing.
git clone https://github.com/jspaper22/bftdetector.git
```bash
#  SECTION 2: Handling Git Submodule Issue (when cloning into existing repo) 

## Navigate into the cloned bftdetector directory to prepare it.
cd bftdetector

## Deactivate any currently active Python virtual environment.
### This is important before modifying files related to the project's structure.
deactivate

## Remove the hidden '.git' directory inside the 'bftdetector' folder.
### This prevents Git from treating 'bftdetector' as a separate submodule.
rm -rf .git

## Go back to the parent directory (your 'Wiresharks' repository root).
cd ..

## Add the 'bftdetector' folder (now treated as regular files) to Git's staging area.
git add bftdetector

## Set your global Git user email. This identifies you as the author of commits.
### Replace "your_email@example.com" with the email associated with your GitHub account.
git config --global user.email "your_email@example.com"

## Set your global Git username. This identifies you as the author of commits.
### Replace "Your Name" with your desired name for Git commits.
git config --global user.name "Your Name"

## Commit the changes. This saves the added 'bftdetector' content to your local Git history.
### The message describes the changes.
git commit -m "Add bftdetector project content to Wiresharks"

## Push the committed changes from your local 'main' branch to the 'origin' (GitHub) remote.
### You will be prompted for your GitHub username and Personal Access Token (PAT) as the password.
git push origin main
```bash
#  SECTION 3: Python Virtual Environment Setup and Dependency Installation Attempts 

## Navigate into the bftdetector project directory to work on its dependencies.
cd ~/Wiresharks/bftdetector

## Check available Python 3 versions in the system's bin directory.
### This helps identify which Python version to use for the virtual environment.
ls /usr/bin/python3.*

## Attempt to create a Python virtual environment named 'venv'.
### This isolates project dependencies from the system's Python packages.
### This command might initially fail if 'python3-venv' is not installed.
python3 -m venv venv

## If the above command fails with 'ensurepip is not available', install 'python3-venv'.
### This package provides necessary components for creating virtual environments.
sudo apt install -y python3-venv

## Delete the problematic or incomplete 'venv' directory.
### This ensures a clean slate for creating a new virtual environment.
rm -rf venv

## Re-create the Python virtual environment named 'venv'.
### This should now succeed after 'python3-venv' is installed.
python3 -m venv venv

## Verify that the 'pip' executable exists within the newly created virtual environment.
### This confirms the virtual environment was created correctly.
ls -l venv/bin/pip

## Activate the Python virtual environment.
### Your terminal prompt should change to include '(venv)' indicating it's active.
source venv/bin/activate

## Install a specific older version of setuptools as required by the bftdetector project.
### This is run inside the activated virtual environment.
### Initial attempts might have syntax errors if '(venv)' is typed as part of the command.
(venv) pip install "setuptools<58.0.0"

## Install Node.js version 16.x and other necessary system libraries.
### Node.js is needed for Puppeteer, a web automation tool used by bftdetector.
### curl downloads the NodeSource setup script.
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo bash -
### apt installs the Node.js package.
sudo apt install -y nodejs
### Install various development libraries required for GUI and other functionalities.
### Note: 'libgconf-2-4' often fails to locate on newer Kali versions, which is expected.
sudo apt install -y git curl libgtk2.0-0 libgtk-3-0 libnotify-dev libnss3 libxss1 libasound2 libxtst6 xauth xvfb libgbm-dev

## Attempt to install the bftdetector project itself using its setup.py/pyproject.toml.
### This command installs all dependencies listed in the project's configuration files.
### This is run inside the activated virtual environment.
(venv) pip install .
```bash
#  SECTION 4: Docker Related Commands (Attempted on Host, but not successful due to virtualization) 

## Check Docker daemon status.
### Used to verify if Docker Desktop is running and accessible from WSL.
docker info

## Shutdown all WSL distributions.
### Used as a troubleshooting step to restart WSL and potentially resolve Docker connection issues.
wsl --shutdown # This command is run from Windows Command Prompt or PowerShell.

## Pull an Ubuntu 20.04 Docker image.
### This was intended to create a compatible environment for bftdetector.
docker pull ubuntu:20.04

## Run an interactive Docker container based on Ubuntu 20.04.
### This would have given a shell inside the isolated environment.
docker run -it --name bftdetector_env ubuntu:20.04 /bin/bash

## Commands to start/enable Docker service within a Linux system (not applicable for WSL).
### These were attempted before realizing WSL's Docker integration requires Docker Desktop for Windows.
sudo systemctl start docker
sudo systemctl enable docker

### The system's BIOS/EUFI had to be manipulated in order to get the docker to run. This couldn't be done, leaving us at a dead end.