# Local environment setup with remote dev desktop

There are [many different local environment solutions](https://docs.acquia.com/blt/install/local-development/).
For the purpose of this exercise we are going to use [BLT](https://docs.acquia.com/blt/) with [Dev Desktop](https://docs.acquia.com/dev-desktop/).
 
Acquia Dev Desktop provides the quickest way to configure and run Drupal for local development on your Mac or Windows PC. 
Acquia Dev Desktop is an xAMP stack (or DAMP stack) installer, providing a full Drupal-specific stack that includes Apache, MySQL, and PHP. 

Also, because of its integration with Acquia Cloud, Acquia Dev Desktop provides the easiest method to publish, develop, and synchronize your local Drupal websites onto the web.

Check if you have the following system requirements: \
() open your terminal.\
() git \
`git`\
If you do not have git download here: https://git-scm.com/download/win \
() composer \
`composer -V` \
If not download the latest version of [composer](https://getcomposer.org/doc/00-intro.md#installation-windows).\
() PHP 7.3 - \
`php -V` \
If you do not have php download from here: https://www.foxinfotech.in/2019/01/how-to-install-php-7-3-on-windows-10.html \
() BLT https://docs.acquia.com/blt/install/ \
() After any new installs please restart your terminal. \
() Windows Subsystem \
() Drush \
`drush -V` \ 
If you do not have drush \
```
wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar \
chmod +x drush.phar \
sudo mv drush.phar /usr/local/bin/drush \
sudo cp /usr/local/bin/drush /usr/local/bin/drush.bat
```

## Step one: Fork the repo
Go to https://github.com/AllieRays/dev-assessment and fork the repository to a sites directory on your local machine.

## Step two: Download Dev Desktop
Obtain a free version of the [Acquia Dev Desktop](https://dev.acquia.com/downloads) program.

## Step three: Downloand [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)
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
`sudo apt-get install -y php7.3-cli php7.3-curl php7.3-xml php7.3-mbstring php7.3-bz2 php7.3-gd php7.3-mysql mysql-client unzip git`

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


## Step three: Create ssh keys with Dev Desktop and add them to github.
https://docs.acquia.com/dev-desktop/config/keygen/  \
() Create key  \
... () On the Acquia Dev Desktop menu, click Preferences.   \
... () On the General tab, click Generate.   \
........ * do not add a password  \
........ * Key password is empty. Do you really want to save your private key unencrypted? click YES  \
........* name your key dev_assessment_key and save to your .ssh directory.  \
() Add your key to your github account.  \
... () Go to https://github.com/settings/keys and add a new ssh key  \
....() save the key as dev_assessment_key \
....() type in `ssh-agent -s your_key_name` \
() Symlink your ssh key to your WSL `ln -s /mnt/c/Users/yourname/.ssh ~/.ssh`

## Step four: Clone your repo with SSH
`git clone git@github.com:[your-github-handle]/dev-assessment.git`

## Step five: Composer
Run Composer to install dependencies  \
`composer install`
or 
`php -d memory_limit=-1 /usr/local/bin/composer install`


## Step six: Add mysql to your path
nano ~/.bashrc and add the following lines.
```
export PATH="C:/Program Files (x86)/DevDesktop/mysql/bin:$PATH"
export DEVDESKTOP_DRUPAL_SETTINGS_DIR="$HOME/.acquia/DevDesktop/DrupalSettings"
```


## Step seven: Set up Acquia dev desktop
Select with an existing Drupal site located on my computer\
Fill the following fields  \
() Local codebase folder: `[your-path]/dev-assessment/docroot`   \
() Local sitename: dev-assessment   \
() Use PHP: 7.3.9   \
() Database: Start with an sql dump file. Dump File: dev-assessment04302020.sql \
() New Database name: dev_assessment 


## Step Eight: Install Drush globally 
wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar \
chmod +x drush.phar \
sudo mv drush.phar /usr/local/bin/drush \
sudo cp /usr/local/bin/drush /usr/local/bin/drush.bat

## Step nine: BLT setup 
() cd /sites/dev-assessment/docroot \
() run `blt setup` \
() y \
() y 

## Step ten: drush into the site
Once you are done go back to the dev desktop. 

### Troubleshooting 
SSH KEY public-key permission denied 

#### Composer Issues 
Delete the core and vendor directories so that composer can redownload them for you. 
`rm -rf docroot/cor` \
`rm -rf vendor`

