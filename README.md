# Piker Bot

Stock trading bot for executing swing trades over days to weeks. 

## Features
- Reads queued trades from a Google spreadsheet in my Google drive and adds them to local sqlite3 database
- Heartbeat pulses every minute and checks the price on stocks being traded.
- Bot purchases the stock when it falls below the entry price while still being above the stop loss and the closing price from the previous heartbeat pulse.
	- This is to ensure the stock is bought when a potential upwards trend has started. Does not buy if the stock goes straight down from the entry price to the stop loss.
- Bot will sell the stock when the stop loss is hit. If the exit price is hit, it will wait until the price drops below the closing price from the previous heartbeat pulse.
	- No point in selling if the stock is just going up with every heartbeat pulse. We wait for a shift in trend to sell.
- As the trade progreses, the bot automatically updates the sqlite3 database and the trade journal in Google Drive.

## Libraries
Requires a number of libraries available on pip as well as a plotly-orca installation on your PATH.

## Configuration and Installation
- Clone the [Stock Library](https://github.com/adam-long-tech/stock-libraries) repo and follow the README instructions to install locally with pip.
- Clone the piker-bot into the same parent directory containing stock-libaries.
- Copy the example_configuration.py file and rename it bot_configuration.py
- Follow the notes in bot_configuration.py to configure the bot properly.
- The Google Drive API will provide instructions on how to activate the API on a first run.

## Running the Bot

I had a docker image, but it was too difficult to get the logging to work with crontab, so it has been sidelined for the time being.

You can execute main-pulse.py to fire the heartbeat pulse every minute or run main-scheduler.py to activate
the scheduler and begin pulsing the heartbeat every minute for an eternity.

