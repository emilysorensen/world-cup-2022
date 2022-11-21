# Worldcup Slack Bot

WorldCupBot will notify a Slack channel/group for every matches during a FIFA World Cup.

The API haven't changed since the Russia World Cup 2018.
Which means you can use that bot for every FIFA World Cup, you just need to update `ID_COMPETITION` & `ID_SEASON`.

### Find the competition you are looking for

World Cup | `ID_COMPETITION` | `ID_SEASON`
------------ | ------------- | -------------
FIFA World Cup Russia 2018™ | 17 | 254645
FIFA U-20 World Cup Poland 2019 | 104 | 281971
FIFA Women's World Cup France 2019™ | 103 | 278513
FIFA World Cup Qatar 2022™  | 17 | 255711

If the competition you are looking for isn't defined below, here is how you can find these numbers:

- determine when the competition will start (for example `2022-11-19T00:00:00Z`)
- go to `https://api.fifa.com/api/v3/calendar/matches?from=DATE_START&language=en&count=500` and replace `DATE_START` with the previous date (be careful to use the same format)
- look for the competition (for example `FIFA World Cup Qatar 2022`)
- get the correspondant values:
  - `IdSeason`
  - `IdCompetition`

### What it does

That bot is using the "unofficial" FIFA json API (the one used for their mobile apps).

It will post a message :
  - when a match starts
  - for every red/yellow card
  - for the half time and end time
  - and of course, for every goal

### Preview

Here is a preview of the Colombia vs Japan match during the Russia World Cup 2018.

![worldcup-slack-bot sample](https://i.imgur.com/H5kUavh.png)

### Requirements

  - PHP >= 5.5 (I guess?)
  - You need to create a Slack Apps with an incoming webhooks:
    - Jump at https://api.slack.com/messaging/webhooks (you have to login)
    - Create a Slack app
    - Enable Incoming Webhooks
    - Create an Incoming Webhook (you'll then select the channel used for that bot)
    - Grab the link like `https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX` and put it in `SLACK_URL`

### Installation

  - Clone this repo
  - Set up a cron to run every minute:

  ````
  * * * * * cd /path/to/folder && php worldCupNotifier.php >> worldCupNotifier.log
  ````

### Side notes

The code is ugly but it works.

Everything is posted in french, but feel free to fork and use your own language. FYI, FIFA API can provide text in en/fr/de/es/pt.
