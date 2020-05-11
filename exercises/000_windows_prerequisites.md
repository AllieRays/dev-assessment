## Acquia BLT with DDev for Windows with all Prerequisites as of May 8 2020 

Required prerequisites  
* Windows 10 build 1909
* Admin permissions 

At the end of this exercise the following system requirements should be setup \
() Windows 10 build 1909 with Admin permissions and Hyper V enabled\
() A windows package manager \
() Docker \
() Docker Compose 1.21.0 and higher  \
() WSL (using bash) \
() PHP 7.3 (on windows and WSL) \
() GIT (windows and WSL) \
() SSH keys (WSL) \
() A text editor like sublime 

## Docker 
Install [Docker](https://www.docker.com/community-edition)  version 18.06 or higher for Windows 

-   docker-compose 1.21.0 and higher (bundled with Docker in Docker Desktop for Mac and Docker Desktop for Windows)
    -   Windows 10 64-bit Pro or Enterprise with  [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/) 
-   Hyper-V and Containers Windows features must be enabled.
-   The following hardware prerequisites are required to successfully run Client Hyper-V on Windows 10:
    -   64 bit processor with  [Second Level Address Translation (SLAT)](http://en.wikipedia.org/wiki/Second_Level_Address_Translation)
    -   4GB system RAM
    -   BIOS-level hardware virtualization support must be enabled in the BIOS settings. For more information, see  [Virtualization](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled).
    -   Windows 10 build 1909
 
 
### Docker Settings 
once docker is downloaded start docker desktop \
then from the toolbar icon right click settings \
Click on "Switch to Linux Containers" \
Then Click on settings \
() change the following settings \
... () start docker deskop when you log in \
... () expose daemon ton tcp://localhost:2375 without TLS \
..... () Navigate to Resources -> File Sharing \
..... () Check C drive \
..... () Apply and Restart Docker 


## Windows Dependency Package Manager Chocolatey
Copy the following text and paste it into powershell
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) 
```
() Wait a few seconds for the command to complete. \
() If you don't see any errors, you are ready to use Chocolatey! Type  `choco`  or  `choco -?`  now, or see  [Getting Started](https://chocolatey.org/docs/getting-started)  for usage instructions.


## PHP 7.3
`choco install php --version=7.3.0` \
update your php.ini file located at `C:\tools\php73\php.ini` \
update your memory_limit to `256M` \
remove `;`to uncomment `extension=gd2` 

## Composer 
Install composer globally \
`choco install composer`

## WSL 
Download [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about) \
You must create a UNIX username with a password when prompted at the end of the installation process. Certain Acquia BLT  commands will not function if you install the Windows Subsystem for Linux using an account without a password.

To install the required applications for Acquia BLT (including PHP, Node.js, Git, and Composer), run the following commands:
Run the following command, and press Enter when prompted:
`sudo add-apt-repository ppa:ondrej/php`

Run the following command:
`sudo apt-get update`

Run the following command, based on your installed version of Acquia BLT:
`sudo apt-get install -y php7.3 php7.3-cli php7.3-curl php7.3-xml php7.3-mbstring php7.3-bz2 php7.3-gd php7.3-mysql mysql-client unzip git`

Run the following command:\
`php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"`

Run the following command:\
`php composer-setup.php`

Run the following command:\
`sudo mv composer.phar /usr/local/bin/composer`

Run the following command:\
`curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -`

Run the following command:\
`sudo apt-get install -y nodejs`

Install Python 3 and PIP.
`sudo apt-get install -y python3 python3-pip`

Install Docker Compose into your user's home directory.
`pip3 install --user docker-compose`


### Ensure Volume Mounts Work
WSL, windows and docker do not play nice together with file path sharing. We need to fix that. Create a wsl.conf file
`sudo nano /etc/wsl.conf`
```
[automount]
root = /
options = "metadata"
```
save and close 


() Configuring Git \

Before working with an Acquia BLT project, you must identify yourself to Git by running the following commands:\
`git config --global user.email "you@example.com"`\
`git config --global user.name "Your Name"` \
If you haven’t already configured an SSH identity (useful for working with projects on GitHub and interacting with your websites on Acquia Cloud), you should generate an SSH key.

() Add function to .bashrc file 
inside the Windows Subsystem \
`nano  ~\.bashrc`\
add this function
```
function blt() {
  if [ "'git rev-parse --show-cdup 2> /dev/null'" != "" ]; then
    GIT_ROOT=$(git rev-parse --show-cdup)
  else
    GIT_ROOT="."
  fi

  if [ -f "$GIT_ROOT/vendor/bin/blt" ]; then
    $GIT_ROOT/vendor/bin/blt "$@"
  else
    echo "You must run this command from within a BLT-generated project repository."
  fi
}
```
source ~/.bashrc


## Restart your computer
() Save and close and restart your computer. \
() Once the windows machine is up and running restart docker and check the settings listed above \
Everything else will be done again with Unbuntu 

---

# Ubuntu configuration 

## Install Docker for Ubuntu virtual box 
[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)
open wls as admin
```
bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get install ca-certificates
sudo apt-get install curl
sudo apt-get install gnupg-agent
sudo apt-get install software-properties-common
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Verify that Docker Engine is installed correctly by running the  `hello-world`  image.
```
 docker run hello-world
```

## Create your ssh keys 
Open your wsl terminal as admin and create an ssh key.\  
`bash`
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` \  
() cd to your ssh file \  
... () Go to https://github.com/settings/keys and add a new ssh key  \  
....() save the key as username_public_key on github \  
() cat your key ` C:\USERS\[username]\.ssh` \  
() Add your key to your github account.  \  
... () Go to https://github.com/settings/keys and add a new ssh key  \  
....() save the key on github \  
....() in your wsl terminal type in `ssh-agent -s id_rsa`

## Install a text editor Sublime or equivalent 
https://download.sublimetext.com/Sublime%20Text%20Build%203211%20x64%20Setup.exe
