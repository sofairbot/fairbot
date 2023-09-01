# What's that

Fairbot is the first bot designed to bring fairness in the world of sorare

# How does it work

Fairbot is a set of plug and play scripts you can download and run with nodejs (more on that further)

Pick the script of your choice and you are up !

# Step-by-step

## Setup

This has to be done once and for all

### Nodejs

This is the development language used by the scripts. You need it to launch them. It's free, open-source and run on all computers

Install it once and for all from the official website : https://nodejs.org/en/download

Recommended installer for a Windows computer : https://nodejs.org/dist/v18.17.1/node-v18.17.1-x86.msi

### Workspace

Create a folder on your computer to run fairbot

Recommended : `C:/fairbot/`

### Run

* Download and run the script of your choice in this folder
* Open a command line in that folder following this tutorial https://www.lifewire.com/open-command-prompt-in-a-folder-5185505
* Run the command  `node name_of_the_script.build.js`


## Test all is ready

This script is intended to test your nodejs installation

* Open a command line in that folder
* run `node --version`

You should see the version displayed

Nice. Let's try a fairbot script.

* Download fairbot-test.build.js
* Put it in the workspace
* Open a command line
* Run the command  `node fairbot-test.build.js paweltrader`

You should see the number of football cards paweltrader owns. 
You can change to any username.
This username is special : it's called a **slug**. You can get it from the web page of a user gallery. All lowercase, without spaces.

`https://sorare.com/football/gallery/paweltrader/cards`

# Script list

## fairbot-test

Test your installation and connectivity with sorare api
