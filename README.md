# SolarAndPowerDraw
Some quick stuff for doing calculations related to solar power generation and power draw. This is Germany.. so there are some specifics to the conclusions (like an electricity price of at least 25 Cents/kWh).

# Intro
I found it to be fiendishly difficult to determine whether or not to install solar panels. If so, how many? Do I add a battery? What about the electric car?  
As often the case, one needs data to come to qualified conclusions. So here we go... I made it a science project. 


# Setup
There is 
- a SDM630 three-phase power meter measuring mains power draw. Measurements are taken via Modbus and a Raspberry Pi running [goSDM](https://github.com/gonium/gosdm630).
- a 250 Watts peak no-name solar panel connected to the grid via an Envertech Inverter. Power generation is measured with a [Shelly Energy Meter](https://shelly-api-docs.shelly.cloud/#shelly-em). The panel had been installed west-facing for about one year (65 degrees inclination). I've now changed it to south-facing at 45 degrees inclination).
- an instance of [fhem](https://fhem.de/) doing the logging for both energy/power meters.
- an electric car consuming about 17.3 kWh/100 km.

# Python Scripts for Making Sense of the Data
fhem does some plotting. These plots are good for a quick glance. And while there are many possible solutions with fhem (there's a module for electricity metering) I'm not much of a Perl guy. So I decided to hack something in Python. Not neccessarily nice but it works.

## Log file Conversion from fhem to csv
fhem does logging with one item per line. That's a bit inconvenient for looking at the data in Excel (or whatever one may use to do some quick plots/aggregation). So we'd love to see the data in another format: csv. A timestamp at the beginning of the line and all data thereafter.
### SDM Data
### Shelly EM Data

# Quick Conclusion(s)
- If you're seeing a (more or less) constant power draw of your house above a certain level (say 250W): Get a solar panel with a direct inverter (feeding into the house eletrical installation). This will pay off in seven to ten years (at current (2021) electrity and panel/inverter rates). Each additional 25 Euros will roughly add another year for arriving at break-even. So keep additional costs down:
  - Short cable lenghts for feeding into the electrical installation of the house (copper is expensive).
  - No power meter for measuring power generation.
  - Do not try to generate more power than you need.
  - Do not try to sell electricity back to your provider ("Einspeiseverg??tung").
  - Try to do most of the work yourself. (I know: You should also pay yourself. If I go with a rate of 120..150??? per hour for my engineering... go figure if it will ever reach break even...).
  - If you need an electrician (you probably will because we're in Germany): Try to get hold of a friend of a friend...
  - Go cheap on the mounting: If you can, skip it. (Another year waiting for break even to happen.) Just take some wood bars to build a frame and a 25kg sandbag as ballast.
- Having an installation facing west gives you approximately 65% of power generation vs. an installation facing south. 
- A 250 Watts peak no-name panel gives approx. 200 Watts peak south facing at 45 degrees inclination. If it's a sunny day you'll have a maximum of 1,6 kWh of power generation. That makes for approx. 25..35 Euros per year of electricity cost cut by generating you own power.
- It took me about an hour to get hold of the conformity declaration for the inverter and filling in the necessary (simplified, because less than 600 Watts) paperwork for "legalizing" my 250 Watts peak plug-in panel (declaring it at the utility running the local grid and at the federal agency (Bundesnetzagentur). Again: This is 120..150 Euros per hour of my time. Doohh... 
- Larger installations will only make sense if you're scaling to a level where you're doing this as a business:
  -  Long story short: You won't make a profit from power generation (and/or consuming your own power thus cutting the electricity bill). Instead, you'll rely on tax savings by writing off the installation and getting back sales tax ("Umsatzsteuer") from the tax office. You'll end up paying sales tax on your self-generated power, though.
  -  If you include a battery: Keep it small. Just big enough to store most of the power generated on a sunny day. But not everything (remember the base load of the house). Oversizing the battery adds a lot of cost that won't generate any benefit for you. And you'll want to be able to make a case for selling back electrical power to the grid so you can convince the tax office of having the goal of making money from that.
