# DiscordSpeechBot
A speech-to-text bot for discord written in NodeJS.

## Create a Discord Bot
1. Go to the Discord Developer Portal
    Your first step is to browse over to the Discord Developer Portal: https://discordapp.com/developers/applications/
    This portal shows all of your applications and bots.
    If you already have a bot created, click it in the list. If you don’t have any discord bots, click the “New Application” button.

2. Give Your Bot a Name
    Here you’ll be prompted to give your application (bot) a name.
    You’re likely making a Discord Bot here, or you need your token for a Discord Bot. If this is true, then think about what you want your bot to be named and enter it here.
    
3. Bring Your Bot to Life With an Icon and Description
    Awesome! You’ve created your very first Discord Application! The only thing left is to bring your bot to life by giving it a description and an icon.
    Add Your Discord Application Icon And Description - The best size for your bot’s icon is 1024×1024 pixels, but you can go lower and achieve quality results. I personally go with 512×512 most of the time (based on the icons I choose).
    
4. Retrieve Your Token
    Your next step is to go over the menu on the left side of the screen and click “Bot”. It’s the icon that looks like a little puzzle piece.
    Discord Development Portal - Browse To The Bot Tab: Now you want to click the blue “Add Bot” button.
    Discord Bot - Click Add Bot: Click the “Yes, do it!” button,
    Discord Bot - Add Bot To This App Dialog: You’ll see a green message, “A wild bot has appeared!”. You’ll also see a “Token” and a blue link you can click called “Click to Reveal Token”. As soon as you click this link, your token will be revealed.
    Discord Bot - A Wild Bot Has Appeared!: And that’s it! You have your token!

5. Add Your Bot to a Discord Server
    In order to add your bot to your Discord Server, you’ll need to navigate back to the “OAuth2” tab.
    Discord Bot Token - Oauth2 Screen: Once there, scroll down to the “Oauth2 URL Generator” section. In the “Scopes” section, you’ll want to select the “bot” checkbox.
    Discord Bot Token - Oauth2 Url Generator: You’ll notice that a URL appeared as soon as you clicked “bot” — this will be your URL for adding your bot to a server.
    Scroll down some more to the “Bot Permissions” section. This is where you choose what permissions to give your bot, and what it can and can’t do.
    Discord Bot Permissions Checkbox Selection: Based on what type of bot you’re planning on building, you’ll want to select permissions that most closely match what it’ll be doing day-to-day.
    Important: Do not select all of the permissions “just to make things easy”. Your permissions are the second line of defense in case somebody gets their hands on your bot token. Only give your bot the permissions it really needs, that way you lower the risk of compromising your server. After you’ve selected your permissions, scroll up a little bit and look at the URL that was generated.
    Discord Bot Authorization String: Click the blue “Copy” button on the right side. This is the URL you’ll navigate to in order to add your bot to a server. Go to that URL and you’ll see a page that looks sort of like this (see below). Here you’ll want to select the server you’re adding your bot to, double-check the permissions you’re giving your bot, and then continue to the next step.
    Discord Bot - Add Bot To Server (Authorize): You’ll likely get an “I’m not a robot” captcha message on the next screen. Solve the captcha and continue.
    Discord Bot Captcha Message (Not A Robot): Success! Your bot has been authorized, and you should see it pop up in the list of participants on your server!



## Deploy your code to Heroku
If you don't have a linux server/machine then you can use Heroku for hosting your bot 24/7 and it's free.
Under "Resources" tab, use the "worker" dyno type, and not the "web" one. You will need to configure the "Config Vars" under "Settings" tab, these are the environment variables from the settings section below.

Tutorial: https://dev.to/codr/discord-ears-bot-on-heroku-4606
1. Create and login to your Heroku account (https://heroku.com/). It is free and no credit card required.
2. Make a new app, give it some name and set your region:
3. The easiest way to deploy the code is by forking the Github repository, a copy of the repo will be added to your Github account which you can use. Alternatively you can use Heroku CLI tools, but that's beyond our scope and for advanced users only.
4. Once forked, select GitHub as deployment method and connect the DiscordEarsBot repository.
5. Scroll down and click on "deploy branch". It might take a minute or two until it's done.
6. Now we need to provide some API keys for the bot. Go to the settings tab and click to reveal the config vars.
7. Here you have to provide the necessary API keys as key-value pairs.The "settings" section on Github explains where you can get your API keys from. (The Discord Speech Bot requires two additional API keys.)
8. Go to the Resources tab and you should see two Free Dynos: a web and worker type. You need to disable the web and enable the worker dyno.
9. Now you're ready and set. You can see the output logs from the bot by clicking on "more" and then "view logs".
10. Make sure you've invited/added the bot to your Discord server. In case you haven't, you get the invite link on the developers portal, just open that link in your browser and follow the steps.
11. With the bot invited you can make the bot join a voice channel, and as you speak you'll see logging info on Heroku, and the bot should also be doing its job.


## Installation
You need nodeJS version 12+ with npm on your machine.

## Settings
Create a (free) discord bot and obtain the API credentials (Bot Token).
Here's an easy tutorial: https://www.writebots.com/discord-bot-token/
Note: Give your bot enough permissions or simply grant it Administrator rights.

Create a (free) WitAI account and obtain the API credentials (Server Access Token): https://wit.ai/

Rename the file `settings-sample.json` to `settings.json` and enter the obtained API credentials:
```
{
    "discord_token": "your_token",
    "wit_ai_token": "your_token",
    "reset_url": "your_reset_url"
}
```

If you are using Heroku or another service you can also use Environment Variables instead of a settings file. Configure these with the appropriate values:
```
DISCORD_TOK
WITAPIKEY
RESETURL
```

## Running

Execute the following in your shell or prompt:
```
node index.js
```

Use [PM2](https://www.npmjs.com/package/pm2) to keep the bot running 24/7, it will also restart the bot in case of a crash or on memory limits (2GB default):
```
pm2 start ecosystem.config.js
```

## Usage
By now you have a discord server, the DiscordSpeechBot is running and is a part of your server.
Make sure your server has a text and voice channel.

1. Enter one of your voice channels.
2. In one of your text channels type: `!join`
3. Type `!help` for a list of commands.

Examples:

```
!play https://www.youtube.com/watch?v=vK1YiArMDfg
!play red hot chili peppers californication
!list
!skip
```

### Voice commands

When the bot is inside a voice channel it listens to all speech and tries to transcribe it to text.

### Notes: 
- Each user talks to a separate channel, the bot hears every user separately, and will transcribe each user, tagging each transcribed line.
- Only when your user picture turns green in the voice channel will the bot receive your audio.
- A long pause interrupts the audio input.
- (WitAI only) The duration of a single audio input is limited to between 1 and 20 seconds, longer and shorter audio is not transcribed. generally, the break in speech for breathing is enough separation to give the bot enough time to process.


## Language
WitAI supports over 120 languages (https://wit.ai/faq), however only one language can be used at a time.
If you're not speaking English on Discord, then change your default language on WitAI under "settings" for your app.

You can also change the language using the following bot command:

```
!lang <code>

!lang en     for English
!lang es     for Spanish
!lang ru     for Russian
...

The bot should reply with a success message.

<code> should be an ISO 639-1 language code (2 digits):
https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
```

### API Swap

By default WitAI's free API is used for voice recognition / transcription. But you can easily integrate any other API into the bot. You can use Google's Speech-to-Text API as follows:

1. Open `index.js`, inside the function `transcribe(file)` make sure that `transcribe_gspeech` is being used and the other one(s) are disabled.
2. You may want to adjust the `languageCode` value if you're speaking a non-English language.
3. Enable Google Speech API here: https://console.cloud.google.com/apis/library/speech.googleapis.com
4. Create a new Service Account (or use your existing one): https://console.cloud.google.com/apis/credentials
5. Create a new Service Account Key (or use existing) and download the json file.
6. Put the json file inside your bot directory and rename it to `gspeech_key.json.
