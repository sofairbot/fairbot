# What's that

* Do you relist your cards manually? **Unfair**
* Do you stack predefined marketplace filter to find a card on sale? **Unfair**
* Do you spend hours finding cards to offer to? **Unfair**
* Do you struggle using sorare's website poor UX? **Unfair**

Fairbot is the first bot designed to bring fairness in the world of sorare.

It is composed of a set of plug and play scripts you can download and run with your computer

It's free. 

You can of course by me some coffees to support me : [buy me a coffee](https://www.buymeacoffee.com/jeremylavi)

# How does it work

Setup your workstation once and for all

Download the script of your choice and you are up !

# Does it need my credentials ?

Some do, some don't. There's no magic here. It can't list your card without credentials...

If the script requires to access private information about your accounts, like, your current balance, it needs your email and password.

If the scripts requires to perform transactions (listing, buying, bidding), it requires your starkware private key as well.

# Security warning

- **Do not share your config.json file**
- **Do not accept scripts from discord or any other download source**
- **Do not send screenshot of your computer**
- **Do not ask for help publicly**
- **Send me a DM for any question**

# Step-by-step

## Setup

This has to be done once and for all

### Nodejs

This is the development language used by the scripts. You need it to launch them. It's free, open-source and run on all computers

Install it once and for all from the official website : [https://nodejs.org/en/download](https://nodejs.org/en/download)

Recommended installer for a Windows computer : [https://nodejs.org/dist/v18.17.1/node-v18.17.1-x86.msi](https://nodejs.org/dist/v18.17.1/node-v18.17.1-x86.msi)

### Workspace

Create a folder on your computer to run fairbot

Recommended : `C:/fairbot/`

### Run

* Download and run the script of your choice in this folder
* Open a command line in that folder following this tutorial [here](https://www.lifewire.com/open-command-prompt-in-a-folder-5185505)
* Run the command  `node name_of_the_script.build.js`


## Test all is ready

This script is intended to test your nodejs installation

* Open a command line in that folder
* run `node --version`

You should see the version displayed

Nice. Let's try a fairbot script.

* Download [fairbot-test.build.js](https://github.com/sofairbot/fairbot/releases/download/release/fairbot-test.build.js)
* Put it in the workspace
* Open a command line
* Run the command  `node fairbot-test.build.js paweltrader`

You should see the number of football cards paweltrader owns. 

```
limited 105717
rare 40774
superRare 2849
unique 492
```

You can change to any username.

This username is special : it's called a **slug**. You can get it from the web page of a user gallery. All lowercase, without spaces.

`https://sorare.com/football/gallery/paweltrader/cards`

## Setup credentials

### How does it work

This setup has to be run once and for all. Only required if you plan to run authenticated scripts (see script listing below)

It creates a file named `config/fairbot-config.json` with your bot/scripts credentials and configuration

Under the hood, it processes all required by sorare itself [here](https://github.com/sorare/api)

### Generate it

Run it using the command `node setup.build.js`

It requires : username (email), password and your gallery (to extract your slug from it)

You can enter anything, it does not validate anything, just goes through all sorare api generation process. Try with bullshit it works. But will fail later if a script requires credentials... 

**Never, EVER, share this file content**

### Open it

You can open the file with any text editor, like Notepad++ (recommanded)

Example of the file once generated :
```
{
  "credentials": {
    "email": "toto@gmail.com",
    "passhash": "$2a$11$x2uvaXYcUFnGJOjFRpQOWOmNCgljQMhTDr1cfGz92TjX27g5IU0/O",
    "mySlug": "paweltrader",
    "starkwareKey": "<enter your starkware private key here>"
  },
  "options": {
    "database": "C:/fairbot/db",
    "currencies": [
      "WEI",
      "EUR"
    ]
  }
}
```

### Add your starkware key

If the script processes transactions, you need to add your starkware private key to sign transactions.

A placeholder is ready in the file. Replace with your private key if you need it. Private key extraction is described in [sorare api website](https://github.com/sorare/api)

**Never EVER send this key**

**Never EVER send this config file to anyone**

From now on, everything is possible.

# Script list

## Available scripts

|Script   | credentials   | starkware key   | destails   | link |
|---|---|---|---|---|
|fairbot-test   | no  | no   |  Test your installation and connectivity with sorare api | [fairbot-test.build.js](https://github.com/sofairbot/fairbot/releases/download/release/fairbot-test.build.js) |
|setup   | yes  |no   |Setup once and for all the configuration required by other scripts |[setup.build.js](https://github.com/sofairbot/fairbot/releases/download/release/setup.build.js)  |
|pro-trades   | no  | no  | Listen to pro trades  | [pros-trades.build.js](https://github.com/sofairbot/fairbot/releases/download/release/pros-trades.build.js)  |

## Details

### fairbot-test

See setup section

### setup

See setup section

### pro-trades

List all pros trades, either a listing or a transaction

There's not many, be patient :)

#### Run

`node pros-trades.build.js`

#### Expected results

`Frenkie de Jong is listing https://www.soraredata.com/manager/frenkie-5ad7f7fe-d3c9-459c-9b1d-3dcc11d7db7b/sections/transactions`

# Who am I

- @JeremyLavi on Twitter
- Working with sorare API for a year
- Unveiling sorare's ugliest issues
- I work for free :)

Most important : sorare knows who I am. In real life. Not hidding from them in any way.
