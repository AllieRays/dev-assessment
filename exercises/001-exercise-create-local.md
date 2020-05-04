# Local environment setup with Windows, BLT and DrupalVM

## System Requirements
Check if you have the following system requirements: \
() open your terminal.\
() git `git`\
If you do not have git download here: https://git-scm.com/download/win \
() version control - for this exercise we will be using github. If you do not have a github username create one. \
() composer `composer -V` \
If not download the latest version of [composer](https://getcomposer.org/doc/00-intro.md#installation-windows).\
() PHP 7.3 `php -V` \
If you do not have php download from here: https://www.foxinfotech.in/2019/01/how-to-install-php-7-3-on-windows-10.html \
() Windows Subsystem \
If you do not have window subsystem for linux please go to step one in this exercise \
() Drush `drush --version` \
If you do not have drush
```
wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar
chmod +x drush.phar
sudo mv drush.phar /usr/local/bin/drush
sudo cp /usr/local/bin/drush /usr/local/bin/drush.bat
```

Versions: Make sure you're running the latest releases of Vagrant, VirtualBox, and Ansible—as of early 2019, Drupal VM recommends: \
() Vagrant 2.2.x \
() VirtualBox 6.0.x \
() Ansible 2.7.x


## Step one: Download [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)
https://docs.microsoft.com/en-us/windows/wsl/install-win10?redirectedfrom=MSDN
Acquia BLT on Windows has the following requirements:

Running a 64-bit version of Windows 10 Anniversary update (build 14393 or greater).

Access to a local account with administrative rights for Acquia BLT’s initial installation.

Windows Subsystem for Linux (installation instructions)

Note

You must create a UNIX username with a password when prompted at the end of the installation process. Certain Acquia BLT commands will not function if you install the Windows Subsystem for Linux using an account without a password.

If you cannot use WSL, you can instead set up virtualization, and then run Acquia BLT in a virtual machine (VM) or container running Windows, based on the following tools:

Docksal: Supports VirtualBox and Docker
Lando: Supports Docker
Installation

To install the required applications for Acquia BLT (including PHP, Node.js, Git, and Composer), run the following commands:

Run the following command, and press Enter when prompted:
`sudo add-apt-repository ppa:ondrej/php`

Run the following command:
`sudo apt-get update`

Run the following command, based on your installed version of Acquia BLT:
`sudo apt-get install -y php7.3-cli php7.3 php7.3-gd php7.3-curl php7.3-xml php7.3-mbstring php7.3-bz2 php7.3-gd php7.3-mysql mysql-client unzip git`

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

## Step two: download vagrant and virtualbox 

Download and install Vagrant \
https://www.vagrantup.com/downloads.html

Download and install Virtualbox \
https://www.virtualbox.org/wiki/Downloads

restart your computer

## Step three: Download cmder for windows
https://github.com/cmderdev/cmder/releases/download/v1.3.14/cmder.zip


## Step four: run cmder as admin
Open Cmder as admin.
In Cmder, right-click on the toolbar, click 'New Console...', then check the 'Run as administrator' checkbox and click Start.
You need to run Cmder as an administrator

run the following command \
`vagrant plugin install vagrant-vbguest` \
 `vagrant plugin install vagrant-hostsupdater`

## Step five: Create ssh keys inside of your cmder terminal and add them to github.
Open your cmder terminal and create an ssh key.\
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` \
() cd to your ssh file \
() cat your key ` C:\USERS\[username]\.ssh` \
() Add your key to your github account.  \
... () Go to https://github.com/settings/keys and add a new ssh key  \
....() save the key as dev_assessment_key \
....() type in `ssh-agent -s your_key_name`

## Step six: Fork the repo
Go to https://github.com/AllieRays/dev-assessment and fork the repository to your personal github account. 

## Step seven: Clone your repo with SSH
`git clone git@github.com:[your-github-handle]/dev-assessment.git`

## Step eight: Add an upstream to your forked repo 
`git remote add upstream git@github.com:AllieRays/dev-assessment.git` \
run \
 `git pull upstream master`

## Step nine: Composer
Run Composer to install dependencies inside the cmder window  \
If you have permission issues use the windows subsystem temrinal to delete project_root/vendor directory \
`composer install` or `php -d memory_limit=-1 /usr/local/bin/composer install` @todo add windows path

## Step ten: Use BLT to configure your environment
If you have BLT installed globally with cmder you can run 
() cd /sites/dev-assessment/docroot \
() run `blt vm` \
() y \
() y 

## Step eleven: Use the VM from now on
`vagrant up` \
`vagrant ssh`
if you have an issue with python add the following command 
`sudo ln -s /usr/bin/python3 /usr/local/bin/python3 `

nano into .bashrc inside of the vm and add 
```bash
function blt() {
  if [[ ! -z ${AH_SITE_ENVIRONMENT} ]]; then
    PROJECT_ROOT="/var/www/html/${AH_SITE_GROUP}.${AH_SITE_ENVIRONMENT}"
  elif [ "`git rev-parse --show-cdup 2> /dev/null`" != "" ]; then
    PROJECT_ROOT=$(git rev-parse --show-cdup)
  else
    PROJECT_ROOT="."
  fi

  if [ -f "$PROJECT_ROOT/vendor/bin/blt" ]; then
    $PROJECT_ROOT/vendor/bin/blt "$@"

  # Check for local BLT.
  elif [ -f "./vendor/bin/blt" ]; then
    ./vendor/bin/blt "$@"

  else
    echo "You must run this command from within a BLT-generated project."
    return 1
  fi
}
```
then source your bash file
`source ~/.bashrc`

## Step twelve: run blt setup
 inside of the VM run 
 `cd /var/www/dev-assessment`
 `blt setup`
 
## Step thirteen: Turn if off and back on again for safe measure 
close your cmdr terminal \
reopen it \
run 
`vagrant halt` \
`vagrant up` \
`vagrant ssh` \
Restart your apache server \
`sudo service apache2 restart` 

## Step fourteen: drush into the site
Once you are done go back to the terminal \
`cd /var/www/dev-assessment/docroot`  \
`drush uli`

# Step fifteen: Configuring Git
Before working with an Acquia BLT project, you must identify yourself to Git by running the following commands:\
`git config --global user.email "you@example.com"` \
`git config --global user.name "Your Name"` \


### Troubleshooting 
SSH KEY public-key permission denied 

#### Composer Issues 
Delete the core and vendor directories so that composer can redownload them for you. 
`rm -rf docroot/cor` \
`rm -rf vendor`

