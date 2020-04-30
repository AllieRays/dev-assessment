# Local environment setup with remote dev desktop

There are [many different local environment solutions](https://docs.acquia.com/blt/install/local-development/).
For the purpose of this exercise we are going to use [BLT](https://docs.acquia.com/blt/) with [Dev Desktop](https://docs.acquia.com/dev-desktop/).
 
Acquia Dev Desktop provides the quickest way to configure and run Drupal for local development on your Mac or Windows PC. 
Acquia Dev Desktop is an xAMP stack (or DAMP stack) installer, providing a full Drupal-specific stack that includes Apache, MySQL, and PHP. 

Also, because of its integration with Acquia Cloud, Acquia Dev Desktop provides the easiest method to publish, develop, and synchronize your local Drupal websites onto the web.


Check if you have the following system requirements:
() open your terminal.  
() composer 
`composer -V`   
If not download the latest version of [composer](https://getcomposer.org/doc/00-intro.md#installation-windows).
() PHP 7.3 - https://www.foxinfotech.in/2019/01/how-to-install-php-7-3-on-windows-10.html
() BLT https://docs.acquia.com/blt/install/


## Step one: Fork the repo 
Go to https://github.com/AllieRays/dev-assessment and fork the repository to a sites directory on your local machine. 


## Step two: Create ssh keys with Dev Desktop and add them to github. 
https://docs.acquia.com/dev-desktop/config/keygen/
() Create key 
... () On the Acquia Dev Desktop menu, click Preferences.  
... () On the General tab, click Generate.  
........ * do not add a password 
........* name your key dev_assessment_key and save to your .ssh directory. 
() Add your key to your github account. 
... () Go to https://github.com/settings/keys and add a new ssh key


## Step two: Clone your repo 
`git clone git@github.com:[your-github-handle]/developer-assessment-exercies.git` 

## Step three: Composer
Run Composer to install dependencies
`composer install`

## Step four: Download Dev Desktop
Obtain a free version of the [Acquia Dev Desktop](https://dev.acquia.com/downloads) program.

## Step five: Add mysql to your path 
nano ~/.bash_profile and add the following lines.
```
export PATH="/Applications/DevDesktop/mysql/bin:$PATH"
export DEVDESKTOP_DRUPAL_SETTINGS_DIR="$HOME/.acquia/DevDesktop/DrupalSettings"
```

## Step Six: Set up Acquia dev desktop
Select with an existing Drupal site located on my computer 
Fill the following fields 
() Local codebase folder: `[your-path]/dev-assessment`  
() Local sitename: dev-desktop  
() Use PHP: 7.3.9  
() Database: Start with an sql dump file  
() Dump File: dev-assessment04302020.sql   
() New Database name: dev_assessment  
