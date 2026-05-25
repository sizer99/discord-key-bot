# discord-key-bot
![Go](https://github.com/ezelkow1/discord-key-bot/workflows/Go/badge.svg?branch=master)

This is a simple golang bot for a discord server that will let members /add spare keys from Steam, Uplay, Origin, GOG, etc. Even URLs for bundles. Then other members can /take keys as they want. It has no rate limits - it is very simple and assumes you trust your users. But you can only let certain roles /take keys if you want.

The commands are:

`/add` - This will open a popup dialog to enter a new game and its key

`/search [match]` - search the game database for anything that matches

`/list` - print a list of all games in the database

`/take` - take a key

Currently, the bot can recognize Steam, Uplay, Origin, PS3, GOG, and URLs. Any other key will be stored as an 'unknown' type.  If a key is Steam or GOG, it will also generate a redemption link on a key `take`.  It remembers who donated each key so they get proper credit.

Finally, the bot supports searching with /search string, comparing a search substring to any key names, essentially a \*(stripped tolower string)\*

If you wish to limit user access this can now be done via discord server controls in the integration section. From there you can limit to channels and user roles for any of the commands or the bot itself.

This was originally written by ezelkow1 on github, and that is archved. I (sizer99) installed it, liked its simplicity, but made a few cosmetic changes, so I've forked it. You can always install the original if you don't like them!  Note - I do NOT actually know golang. But I know enough other C-like languages to be able to mod this.

# Installation

- Download this by grabbing a zip or `git clone https://github.com/sizer99/discord-key-bot`
- Start a text file to hold all the stuff you're going to need to copy!

- Set up Bot on Discord
  - Go to the Discord Developer Applications Portal - https://discord.com/developers/applications - and log in with your discord account.
  - Click 'New Application' in the upper right.
  - Enter a bot name (like 'keybot'), click the checkbox, and Create.
  - Copy the Application ID and save it.
  -  Click 'Bot' on the left, then 'Reset Token'.  Copy the Token and save it, you can never see it again!
  - Click 'OAuth2' on the left, scroll down to OAuth2 URL Generator. 
  - Under 'Scopes' check 'applications.comands' (near the end) and 'bot' (near the start).
  - Under 'Bot Permissions' check 'Send Messages', 'Use Slash Commands', and 'Manage Messages'.
  - At the very bottom copy the 'Generated URL' and save it.

- Set up the code
  - In the discord-key-bot directory, copy conf.json to my_conf.json (or whatever)
  - edit your my_conf.json and set:
  - "Token" is the Token you copied above
  - "DbFile" is any json file you want like "my_keys.json"
  - "GuildID" is the server id for your discord server (right click its icon, Copy Server Info -> Copy Server ID)
  - "AppID" is the Application ID you saved above.
  - Make sure you have the 'golang' package installed. In a Debian derived dist like Mint or Ubuntu, `sudo apt install golang`.
  - Build the app with `go build -buildvcs=false`. If no errors, you're good to go!
  - Finally, run it with `go run github.com/ezelkow1/discord-key-bot -c my_conf.json`.
  - If you see `Bot is now running.  Press CTRL-C to exit.` you're good!

- Add it to your discord server
  - On a browser where you're logged into Discord, paste the 'Generated URL' into a new tab. It'll ask if you want to add this bot to a server. Pick the server you want, okay!
  - If you want, right click your server icon, Settings -> Integrations, find your bot, Manage, and you can choose what roles can use it and what channels it works in.

- Give it a test
  - `/list` and you should see `Empty Database - No Games in Database` in your channel.
  - `/add` and it should pop up a window asking for game name and key. Enter something dummy. It should say `Thank You <yourname> for adding...`
  - `/list` again, you should see the dummy game.
  - `/take <name>` and it should DM you the fake key you entered. `/list` again and nothing left! You're good!

- Set it to run automatically
  - Once you're happy, hit Ctrl-C where you ran the bot to stop the bot.
  - Now run with `nohup go run github.com/ezelkow1/discord-key-bot -c my_conf.json &` to run it in the background even if you log out.
  - You could start it up on reboot with a crontab @reboot entry.

- Multiple servers
  - If you wanted, you could run multiple instances of this with a unique conf file and unique "DbFile" each.


# Versions
| Date | Changes |
| ---  | --- |
| 2026 May 24 | Forked ezelkow1's archive |
| 2026 May 24 | /add message now says what store the key was IDed as |
|             | change /search and /list to use code blocks for aligned output |
|             | cut down on amount of messages /list and /search send (don't send separate count) |
|             | add # Installation section to README.md |



# Archiving Old Version
ezelkow1: I am archiving this repo as of 05/04/2026, I can no longer work on this so archiving it in case people still have it forked/edited.

