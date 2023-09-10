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

There is 2 kinds of scripts :
- listener : listen to real time moves in the platform. Must be always ran to give results. Like, show me what pros are doing real time.
- exec : run and stops by itself after job complete. Like, extract last GW result.

## Available scripts

|Script   | type | credentials   | starkware key   | details   | link |
|---|---|---|---|---|---|
|fairbot-test   | exec |no  | no   |  Test your installation and connectivity with sorare api | [fairbot-test.build.js](https://github.com/sofairbot/fairbot/releases/download/release/fairbot-test.build.js) |
|setup   | exec|yes  |no   |Setup once and for all the configuration required by other scripts |[setup.build.js](https://github.com/sofairbot/fairbot/releases/download/release/setup.build.js)  |
|pro-trades   | listener | no  | no  | Listen to pro trades  | [pros-trades.build.js](https://github.com/sofairbot/fairbot/releases/download/release/pros-trades.build.js)  |
|fairbot   | listener | no  | no  | Listen to player listings  | [fairbot.build.js](https://github.com/sofairbot/fairbot/releases/download/release/fairbot.build.js)  |

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

### fairbot

Track players listings for according to filters. Players can be football, mlb or nba players. 

#### Configuration

To configure your watchers, please go to [Watchers section](#user-content-watchers)

#### Run

Usage : `node fairbot.build.js config/fairbot-config.json`

Try with one of your cards !

#### Hot reload

This scripts hot reload the fairbot-config.json watchers everytime you update the file. No need to restart the bot.

#### Expected results

List all your watchers on startup

```
[14:37:53][setup] baseball watchers
[14:37:53][setup] nba watchers
[14:37:53][setup] football watchers
[14:37:53][watcher] initializing floor-unique
[14:37:53][watcher] initializing limited-gk
```

Prints a log if watcher is configured that way.

# FAQ

### What is the config/fairbot-config.json

This file contains what fairbot is expected to do along with its configuration.

It is divided in 3 sections :
- credentials
- options
- watchers

#### Credentials

This section is generated by the setup.build.js script

#### Options

This section is generated by the setup.build.js script

#### Watchers

This sections describes what fairbot has to watch. It is devided in 3 sections
- football
- baseball
- nba

A typical watcher is composed of :
- a name
- a set of filters
- an action

Example of a fairbot-config.json file with 2 watchers configured. 
*credentials* and *options* sections are optionals and only present if setup.build.js has been executed.

```js
{
  "credentials": [...],
  "options": [...],
  "watchers": {
    "football": [
      {
        "name": "any-unique",
        "filters": {
          "rarity": "unique"
        },
        "log": 10000
      },
      {
        "name": "u23-gk",
        "filters": {
          "position": "Goalkeeper",
          "u23": true
        },
        "open": 20
      }
    ],
    "baseball" : [],
    "nba":[]
  }
}
```
There is 2 watchers here for football sections:
- any-unique : filter any football card of rarity unique. Prints a log if price is under 10000 (1.0000 ETH or 1 ETH)
- limited-gk : filter any football card Goalkeeper u23. Open a browser tab if price is under 0.0020 ETH

Same applies for baseball or nba.

All filters in a watcher stack themselves (combine with a "AND"). A filter with an array as value is obviously a "OR".

List of available filters :

|Filter   | football | nba   | baseball   | value | details |
|---|---|---|---|---|---|
|u23   | yes |no  | no   | true or false | Filter if the card is a u23 |
|position   | yes |yes  | yes   | "Goalkeeper", "Defender", "Midfielder", "Forward", "nba_forward", "nba_center", "nba_guard", "baseball_relief_pitcher", ...  | Filter on the position of the card |
|rarity   | yes |yes  | yes   | "limited", "rare", "super_rare", "unique", "custom_series" | Rarity of the card |
|serial   | yes |yes  | yes   | 1, 2, [...], 5000 | Serial number of the card |
|gift   | yes |yes  | yes   | "referral", "reward" | If the card has been rewarded as a "reward" by sorare. Can be both in an array ["referral", "reward"] |
|season   | yes |yes  | yes   | 2019, ... 2023 | Season of the card. Can be several in an array [2022, 2023] |
|slugs   | yes |yes  | yes   | "kylian-mbappe-lottin" | Slug of a player. Can be several in an array |
|cardTeam   | yes |yes  | yes   | "psg-paris" | Slug of a the team in the card (not actual player's). Can be several in an array |
|cardLeagues   | yes |no  | no   | "ligue-1-fr" | Slug of a league in the card (not actual player's). Can be several in an array |
|team   | yes |yes  | yes   | "psg-paris" | Slug of a the active player team. Can be several in an array |
|leagues   | yes |no  | no   | "ligue-1-fr" | Slug of a the active player team. Can be several in an array |
|uncovered   | yes |no  | no   | true | Allow uncovered card to be matched. Uncovered means any coverage that is not FULL |
|shirt  | yes | no | no | true | Jersey match (jersey match serial) |

**nota bene :** Not configuring uncovered **excludes** uncovered by. Value is false by default (do not match if uncovered).

Examples:

Any football card where the player is wearing Ajax or Real Madrid shirt, from season 2021, even if the player is not eligible anymore. 
Limited only.
Open a browser is selling price is under 0.0010 ETH

```
      {
        "name": "first-watcher",
        "filters": {
          "rarity": "limited",
          "uncovered": true,
          "cardTeam": [
            "ajax-amsterdam",
            "real-madrid-madrid"
          ],
          "season": 2021,
          "serial": 100
        },
        "open": 10
      },
```

Examples:

Disabled watcher
```
      {
        "enabled": false,
        "name": "super-watcher",
        "filters": {
          "rarity": "limited"
        },
        "open": 10
      },
```

You can have as many config file as you want in the `config` folder. Fairbot will pick the one you reference while starting the bot.

### How are prices configured in fairbot

Prices are configured as ETH.

As sorare uses 4 decimals (0.0004), fairbot expect prices without decimals 1/10000 of eth)

To configure 0.0004 eth, just write 4.

### What is a slug and how to get it

A slug is a unique identifier. You've got one for each player, card, league...

The easiest way to get a slug is to go to a page that displays your player and get it from your browser URL:

For Mbappé, go to one of his page [https://sorare.com/football/players/kylian-mbappe-lottin/cards](https://sorare.com/football/players/kylian-mbappe-lottin/cards) to find his slug `kylian-mbappe-lottin`

There is a relation between a player slug and his card's slugs : [https://sorare.com/football/cards/kylian-mbappe-lottin-2021-limited-494](https://sorare.com/football/cards/kylian-mbappe-lottin-2021-limited-494)

You can notice cards slugs are the following : `PLAYERSLUG-SEASON-RARITY-SERIAL`

### More about fairbot ?

Fairbot uses a config file, located in the `config` and a local database located in the `db` folder.

#### config

The config folder stores all your configuration. You can split configurations in different files according to your need. 

Fairbot will only pick ONE config file at a time. Choose carefully while booting fairbot which one to start.

You can store your config files outside this folder if you want, it's up to you. Reference it correctly when starting the bot.

Config files may store your credentials if the `credendials` section is filled. **NEVER GIVE THIS FILE OR ITS CONTENT OR YOU LOOSE YOUR GALLERY**

#### db

This is a local database. Fairbot will store some data required by some scripts, along with your JWT API token, required to access the API while authenticated.

This JWT is named signin-*your-slug*

**NEVER GIVE THIS FILE OR ITS CONTENT OR YOU LOOSE YOUR GALLERY**

Token need to be refreshed sometimes (once a month or so). Delete the file dans reboot the bot to generate a new one.

# Who am I

- @JeremyLavi on Twitter
- Working with sorare API for a year
- Unveiling sorare's ugliest issues
- I work for free :)

Most important : sorare knows who I am. In real life. Not hidding from them in any way.
