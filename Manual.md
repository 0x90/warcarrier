# Installation #

### dependencies (in Debian) ###
This should get us going in DEBIAN (dependencies already installed in WEAKERTH4N LINUX and WarcarrierOS):

```
apt-get update
apt-get install libcurses-perl libjson-xs-perl 
apt-get install libpcap-dev iw build-essential sqlite3-dev
mkdir /tmp/aircrack && cd /tmp/aircrack
svn co http://trac.aircrack-ng.org/svn/trunk/ new
cd new
make && make install
```

### Starting her up ###

Just make sure the terminal is wide enough:

```
svn co https://warcarrier.googlecode.com/svn/trunk/ warcarrier
cd warcarrier
airmon-ng start wlan0 # should make mon0 - change wlan0 to your device
./warcarrier -d mon0 - outputfile
```

You can also do ` ./wcstartup.sh `

### House Cleaning +++important ###

If the Application stops for no apparent reason - this is the result of Curses::UI, the daemons won't runaway! They will be reconnected to Warcarrier upon restart. If you restart warcarrier, it will not spwan a second process for Airodump-NG, Bluetooth, or GPS. It uses the environment (ps aux) to check if they are already running - please ignore the second "Please wait..." status message that will display, this is just the application checking for dependencies.<br /><br />If, however, you do not want to restart Warcarrier after a crash, you should use the Warcarrier cleanup utility ` wcclean `

This utility takes the argument (all|logs|sys|proc)
  * **all** - stops ALL runaway processes and removes ALL logs
  * **logs** - removes all logs and pcap files
  * **sys** - removes all system buffer files created during use
  * **proc** - stops ALL processes used or not used but shared by Warcarrier

# Keyboard Commands #

  * "**s**" for snapshot.
  * "**g**" to reset graph.
  * "**q**" OR "CTRL+C" to quit.
  * "**i**" extra satellite info.
  * "**c**" Catchme-NG! functionality
  * "**u**" Ubertooth Spectrum Analyzer
  * "**x**" exit spectrum analyzer
  * "**r**" Begin/End "Recording" of Bluetooth Spectrum

  * **DEPRECATED**
  * ~~"**b**" add Bluetooth device at any time~~
  * ~~"**h**" for help.~~

# Logging #
All logs will be kept in the ` logs/ ` directory. When Warcarrier finds an AP via Catchme-NG there will be a text log in `./logs/txt ` When Warcarrier asks to "log your adventure", it will be a log in ` ./logs/html` as an HTML file with the Google Map. ./logs/capfiles are the packet capture files from Airodump-NG and ./logs/bluetooth are the capture files from the Ubertooth device.

# Files #
  * **wcstartup.sh** - Autostart script for WarcarrierOS and Weakerth4n Linux - This script will start warcarrier with ` -d mon0 -f file `
  * **wcd** - the Warcarrier GPS|Bluetooth|WiFi daemon.
  * **wcclean** - House cleaning application - run with arguments listed above in **Installation** section
  * **wbt\_pi** - the Ubertooth daemon. This writes to the file ubt.out
  * **warcarrier** - our application
  * **README** - some lame excuse for a README
  * **./logs** - logs directory
  * **./lib** - my OO Perl modules
  * **./includes** - files included for imagery, sorcery, and other