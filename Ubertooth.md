# Ubertooth #

![http://warcarrier.org/images/ubertoothdell.jpg](http://warcarrier.org/images/ubertoothdell.jpg)

<a href='http://ubertooth.sourceforge.net/'><a href='http://ubertooth.sourceforge.net/'>http://ubertooth.sourceforge.net/</a></a>

### dBm ###
The RSSI (received signal strength Indication) is measured in dBm which is to say 1 decibel using milliwatt as a reference. It simply is a power, or intensity measurement of the received signal from the antenna. It is a negative value with (in our case) -100 being the weakest signal strength and going _**up**_ to 0. This means that a -60dBm is stronger than a -90dBm signal, obviously. Bluetooth protocol uses a 1600x/second frequency hopping scheme across a "<a href='http://en.wikipedia.org/wiki/Spread_spectrum'>spread spectrum</a>" of channels which range from frequencies: 2.400GHz to 2.485GHz

Warcarrier now has support for the Ubertooth Bluetooth (spectrum analyzer functionality only) using Dragorn's spectools. I use spectool\_raw to poll the device for the raw dBm values of RSSI  levels. Here is an example of output:

```
-100 -97 -100 -88 -97 -99 -86 -97 -100 ... 
```

These values are preprocessed and dBm values according to the spectools Author himself. I take them and draw lines using the difference in (dBm\_MAX - RSSI\_dBm) yielding (from above output)

```
0 3 0 12 3 1 14 3 0
```

The lines are then made like so:

```
---              |
--         |     |
-90dBm     |     |
-          |     |
--         |     |
---        |     |
--         |     |
-95dBm     |     |
-          |     |
--         |     |
--         |     |
---      | | |   | |
--       | | |   | |
-100dBm _| | |_| | |_
        2400MHz 2406MHz ...
```

Then I simply reverse them into spaces with <a href='http://search.cpan.org/~mdxi/Curses-UI-0.9609/'>Curses::UI</a>'s ` -reverse=>1 ` attribute to the Label object and display them with the corresponding value to the left and a small key in the top right with color coded lines.

This gives a nice clean "zoomed" view of the spectrum, which makes finding a spectral mask tough, but is most accurate because we see _all_ values from -100dBm up to -70dBm.

Each bar is a Curses::UI Label object, which is kind of clunky, but works. So to do this, I used simple logic/magic to convert these bars into one-line bars in a new array, which I invented with a dry-erase marker on my large bathroom mirror.

## Recording ##

In the image below we can see a sample being "recorded" of the site, or surrounding area. This logs the current GPS corrdinates and timestamp with **each** RSSI value seen by the antenna:

<img src='http://warcarrier.org/images/wcapp.png' />

The log is a simple CSV file, which can then be "replayed" at any time in the future. To begin recording simply hit "**r**" and to stop hit "**r**" again. hit "**x**" at anytime to close the Bluetooth Spectrum Analysis window.

## Spectools ##
<a href='http://www.kismetwireless.net/spectools/'><a href='http://www.kismetwireless.net/spectools/'>http://www.kismetwireless.net/spectools/</a></a>



# Testing #
Tested with Ubertooth One and Spectools\_Raw