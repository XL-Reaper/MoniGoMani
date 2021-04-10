```
    ####################################################################################
    ####                                                                            ####
    ###                         MoniGoMani v0.8.1 by Rikj000                         ###
    ##                          ----------------------------                          ##
    #               Isn't that what we all want? Our money to go many?                 #
    #          Well that's what this Freqtrade strategy hopes to do for you!           #
    ##       By giving you/HyperOpt a lot of signals to alter the weight from         ##
    ###           ------------------------------------------------------             ###
    ##        Big thank you to xmatthias and everyone who helped on Freqtrade,        ##
    ##      Freqtrade Discord support was also really helpful so thank you too!       ##
    ###         -------------------------------------------------------              ###
    ##              Disclaimer: This strategy is under development.                   ##
    #      I do not recommend running it live until further development/testing.       #
    ##                      TEST IT BEFORE USING IT!                                  ##
    ###                                                              ▄▄█▀▀▀▀▀█▄▄     ###
    ##               -------------------------------------         ▄█▀  ▄ ▄    ▀█▄    ##
    ###   If you like my work, feel free to donate or use one of   █   ▀█▀▀▀▀▄   █   ###
    ##   my referral links, that would also greatly be appreciated █    █▄▄▄▄▀   █    ##
    #     ICONOMI: https://www.iconomi.com/register?ref=JdFzz      █    █    █   █     #
    ##  Binance: https://www.binance.com/en/register?ref=97611461  ▀█▄ ▀▀█▀█▀  ▄█▀    ##
    ###          BTC: 19LL2LCMZo4bHJgy15q1Z1bfe7mV4bfoWK             ▀▀█▄▄▄▄▄█▀▀     ###
    ####                                                                            ####
    ####################################################################################
```

**WARNING: MoniGoManiHyperStrategy should always be HyperOpted unless you really know what you are doing when manually allocating weights!**   
**MoniGoManiHyperStrategy found in releases already has a decent hyperopt applied to it for BTC pairs!**   
**When changing anything in `config.json` please [re-optimize](https://github.com/Rikj000/MoniGoMani/blob/main/VERYQUICKSTART.md#how-to-optimize-monigomani)!**   

# **Current `MoniGoMani` status @ `v0.8.1`**   

## The idea / Theory:   
MoniGoMani derives iteself from other strategies by it's use of something I called "weighted signals".   
Each signal has it's own weight allocated to it & a total buy/sell signal needed is defined too.   
MGM (MoniGoMani) will loop through all signals, if they trigger it will add up the weight and eventually it will check if it's bigger then what's needed in total, if it is it will buy/sell.   
The beauty lies in using MGM in combination with hyperopting (= backtesting a timeframe a lot of times to find the most ideal values), since all weighted signals have been made hyperoptable it can be used to find the most "ideal" weight divisions.   
Also will it teach us what works where & what doesn't since MoniGoMani first detects Downwards/Sideways/Upwards trends and then does all of the above individually for each kind of trend (Creating basically 3 individual strategies, 1 for each kind of trend).   

## Feature List:   
- *(new)* [Auto-HyperOptable Strategy](https://github.com/freqtrade/freqtrade/pull/4596)! \**(No more need for legacy MoniGoMani, legacy MoniGoManiHyperOpt and MoniGoManiHyperOpted strategy classes)*   
- All Configurable & HyperOptable settings are easily copy/paste-able from the HyperOpt Results
- Configurable & HyperOptable Buy/Sell Signal Weight Influence Tables for Downwards/Sideways/Upwards trends
- Configurable & HyperOptable Total Buy/Sell Signal Percentages for Downwards/Sideways/Upwards trends
- Turn On/Off Trading on Downwards/Sideways/Upwards trends for Buys/Sells *(HyperOptable)*
- Settings to Enable/Disable HyperOpting for individual `buy_params` & `sell_params` through [HyperOpt Setting Overrides](https://github.com/Rikj000/MoniGoMani/blob/main/VERYQUICKSTART.md#hyperopt-setting-overrides)
- Turn On/Off **All** Individual Weighted Signal DataFrame entries for easy debugging in an IDE or better speed while dry/live running or hyperopting
- Each Table has 9 Buy & 9 Sell signals implemented each Configurable & HyperOptable:
  - ADX + Strong Up/Strong Down
  - RSI
  - MACD
  - SMA Short Death/Golden Cross 
  - EMA Short Death/Golden Cross 
  - SMA Long Death/Golden Cross 
  - EMA Long Death/Golden Cross 
  - Bollinger Band Re-Entrance
  - VWAP Cross
- Total Overall Signal Importance Calculator for Total Average Signal Importance Calculation upon the HyperOpt Results
- Main/Sub Plot Configurations for all indicators used *(Handy in FreqUI)*   
   
*\*Support/Updates for Legacy versions stopped since Auto-HyperOptable Strategies are merged into the official Freqtrade Development Branch!*   
***Please switch to the new MoniGoManiHyperStrategy!***   

## Go-To Commands:
For Hyper Opting *(the new [MoniGoManiHyperStrategy.py](https://github.com/Rikj000/MoniGoMani/blob/main/user_data/strategies/MoniGoManiHyperStrategy.py))*:
```properties
freqtrade hyperopt -c ./user_data/config.json -c ./user_data/config-private.json --hyperopt-loss SortinoHyperOptLossDaily --spaces all -s MoniGoManiHyperStrategy -e 1000 --timerange 20210101-20210316
```
For Back Testing *(the new [MoniGoManiHyperStrategy.py](https://github.com/Rikj000/MoniGoMani/blob/main/user_data/strategies/MoniGoManiHyperStrategy.py) or legacy [MoniGoManiHyperOpted.py](https://github.com/Rikj000/MoniGoMani/blob/main/Legacy%20MoniGoMani/user_data/strategies/MoniGoManiHyperOpted.py) or legacy [MoniGoMani.py](https://github.com/Rikj000/MoniGoMani/blob/main/Legacy%20MoniGoMani/user_data/strategies/MoniGoMani.py))*:
```properties
freqtrade backtesting -s MoniGoManiHyperStrategy -c ./user_data/config.json -c ./user_data/config-private.json --timerange 20210101-20210316
```
For Total Average Signal Importance Calculation *(with the [Total-Overall-Signal-Importance-Calculator.py](https://github.com/Rikj000/MoniGoMani/blob/main/user_data/Total-Overall-Signal-Importance-Calculator.py))*:
```properties
python ./user_data/Total-Overall-Signal-Importance-Calculator.py -sc BTC
```
For Hyper Opting *(the legacy [MoniGoMani.py](https://github.com/Rikj000/MoniGoMani/blob/main/Legacy%20MoniGoMani/user_data/strategies/MoniGoMani.py) + legacy [MoniGoManiHyperOpt.py](https://github.com/Rikj000/MoniGoMani/blob/main/Legacy%20MoniGoMani/user_data/hyperopts/MoniGoManiHyperOpt.py))*:
```properties
freqtrade hyperopt -c ./user_data/config.json -c ./user_data/config-private.json --hyperopt-loss SortinoHyperOptLossDaily --spaces all --hyperopt MoniGoManiHyperOpt -s MoniGoMani -e 1000 --timerange 20210101-20210316
```

## **Planned**:   
*Ordered by current schedule/priority*
- If open trade's trend changed for X candles (hyperoptable), check if trade is making losses & send sell signal if it is (To try to unclog the bot & attempt to continue the profit climb :rocket:)   
- **Other & Better indicators!** MoniGoMani has been designed so signals can easily be inserted / swapped out   
Please use the `Total-Overall-Signal-Importance-Calculator.py` (added in `v0.7.1`) to find out which signals do best and report your results to the Discord server, so we can improve! :rocket:
- Individual `BTC_config.json` & `USDT_config.json` files, as well as individual `BTC_MoniGoManiHyperOpted.py` & `USDT_MoniGoManiHyperOpted.py` releases
- Try to get fewer points in the code where the DataFrame gets accessed for speed improvements
- [MultiThreaded DataFrame indicator checking](https://www.machinelearningplus.com/python/parallel-processing-python/) if possible for speed improvements

## **ChangeLog**:  
[View the ChangeLog](https://github.com/Rikj000/MoniGoMani/blob/main/CHANGELOG.md)

## Got Test Results / Ideas / Config Improvements?
- Feel free to join [**CryptoStonksShallRise**](https://discord.gg/xFZ9bB6vEz) on Discord there you can follow/participate in the official channels:
  - `#moni-go-mani-updates`
  - `#moni-go-mani-testing`
  - `#moni-go-mani-help`
  - `#moni-go-mani-setup-releases`

## Need help getting started?
[View the VeryQuickStart](https://github.com/Rikj000/MoniGoMani/blob/main/VERYQUICKSTART.md)

## **Freqtrade**:   
The Bot that makes this strategy possible: https://github.com/freqtrade/freqtrade   
Big thank you to **xmatthias** and everyone who helped on it!