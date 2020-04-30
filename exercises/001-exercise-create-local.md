# Local environment setup with remote dev desktop

There are [many different local environment solutions](https://docs.acquia.com/blt/install/local-development/).
For the purpose of this exercise we are going to use [BLT](https://docs.acquia.com/blt/) with [Dev Desktop](https://docs.acquia.com/dev-desktop/). 
 
Acquia Dev Desktop provides the quickest way to configure and run Drupal for local development on your Mac or Windows PC. 
Acquia Dev Desktop is an xAMP stack (or DAMP stack) installer, providing a full Drupal-specific stack that includes Apache, MySQL, and PHP. 
Also, because of its integration with Acquia Cloud, Acquia Dev Desktop provides the easiest method to publish, develop, and synchronize your local Drupal websites onto the web. 


Check if you have the following 
() composer 
`composer -V`
If not download the latest version of [composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos).
() blt




## Step one: Fork the repo 
Fork the repo the repository to a sites directory on your local machine. 
`git clone git@github.com:AllieRays/developer-assessment-exercies.git`

Clone your repo 
`git clone git@github.com:[your-github-handle]/developer-assessment-exercies.git`


## Step two: Download Dev Desktop
Obtain a free version of the [Acquia Dev Desktop](https://dev.acquia.com/downloads) program.



add mysql to your path 
```
export PATH="/Applications/DevDesktop/mysql/bin:$PATH"
export DEVDESKTOP_DRUPAL_SETTINGS_DIR="$HOME/.acquia/DevDesktop/DrupalSettings"
```




## Step Two: Set up Acquia dev desktop
Select with an existing Drupal site located on my computer.
Fill the following fields
() Local codebase folder: `/Users/allierays/sites/dev-assessment`
() Local sitename:
() Use PHP: 7.3.9
() Database:
() New Database name:



Fork and clone the repository 

