# Raspberry-Wallet-compilation-Guide

manual by Worgon12


1) Installation:
  Raspbian install via SSH on Raspberry
  Sign in with
  User: pi and password: raspberry

  sudo raspi-config set the Raspberry ...
  Keyboard layout, time, password, etc ...

2) Swap memory size (export data to SD card)
  sudo nano / etc / dphys-swapfile

  Simply enter a different value instead of CONF_SWAPSIZE = 100.
  We would recommend 2000, depending on the size of the SD card.
  Save, close and restart.
  = Check Raspberry with htop =

3) System updates:
  sudo apt-get update 
  sudo apt-get upgrade

4) Clean system [from Eugen Meisner]
  sudo apt-get purge $(dpkg -l | awk '/^rc/ { print $2 }') -y
  sudo apt-get autoremove
  sudo apt-get autoclean
  sudo apt-get clean

5) Install dependencies
  sudo apt-get install git screen build-essential libtool autotools-dev autoconf pkg-config libssl1.0-dev libcrypto++-dev libevent-dev libminiupnpc-dev libgmp-dev 
  libboost-all-dev devscripts libdb++-dev libsodium-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev libdb++-dev qttools5-dev-tools libprotobuf-dev 
  protobuf-compiler libcrypto++-dev libminiupnpc-dev qt5-default

6) Wallet = Source Code Download
  git clone https://github.com/CryptoCoderz/Espers.git

7) Compile
  [Explanation ><is always the current directory in the manual, is only intended for a better overview for beginners.]

  cd Espers
 
  >Espers<
  sudo chmod +x src/leveldb/build_detect_platform 
  cd src/leveldb
 
  >Espers/src/leveldb<
  sudo make libleveldb.a libmemenv.a
  cd .. 
 
  >Espers/src<
  sudo mkdir obj (if it was not created automatically, create obj directory)
  make -f makefile.unix USE_UPNP=- -e PIE=1 
  cd ..

  Now compile the QT Wallet with ...
  >Espers< 
  qmake 
  make
 

  Boot the Raspberry into Desktop Mode
  Start Wallet
  finished...
