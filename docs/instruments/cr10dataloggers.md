# Campbell CR10 dataloggers

Notes on using a very old style datalogger from Campbell Scientific.
This requires a bit more effort than newer dataloggers.

## Serial to CS-I/O interface

CR10s have only one serial port on the datalogger panel, and it is not a
standard RS-232 serial port. This means it needs a special interface to
use it rather than just an RS-232 serial connection to an instance of
Loggernet running on a computer. This can be done through CS-I/O-only
devices, such as a Campbell 10KD keypad (see below), or using a special
interface between a computer serial port (standard RS-232) and the
datalogger (CS-I/O). The SC32A is what we use as an interface between
Loggernet and the CR10, either as a direct connection to the
datalogger's CS-I/O port, or connected to it via the 3-ended serial
cable between the CR10 and its storage module.

Once the SC32A is in place, Loggernet should work as normal and a
program can be transferred, data downloaded, input locations monitored,
etc.

## Using the CR10KD

The CR10KD is a keypad and screen that can interface with the CR10. It
is connected to the SC12 cable in series with the datalogger and any
attached storage modules. Once attached, key commands can be used to put
the datalogger in different modes to recieve commands.

### CR10KD keypad commands

* `*0` - Show running table status
* `*5` - View and set clock
* `*6` - View input locations
* `*7` - Display Final Storage data
* `*9` - Storage module commands (download data, etc)
* `*D` - Save/load programs to or from storage module
* Once a mode above has been entered, values in different locations can be accessed with:
  * `A` - advance one location
  * `B` - go back one location`

## Working with Campbell storage modules

Storage modules (SM192, or SM4M) are swapped out at each weather
stations at regular intervals. The full storage modules are then
returned to the lab to download the data, and then erase and test the
module (procedures below).There may be a way to do some of this with the
CR10KD (downloading data at least) in the field but... no idea how.

### Procedure to download data, and erase/test modules in the lab

- Connect the SC32A to a compatible datalogger (CR10, CR23x) and then to the storage module with an SC12 (3 ended) cable. Make sure the datalogger is turned on.
- Connect the other end of the SC23A to a computer's serial port (you will need a 9pin-250pin adapter - and possibly a USB-RS-232)
- Open LoggerNet on the computer and then choose the Storage Module (SMS) application from the menubar.
- There are tabs here for each type of storage module - choose the one that is appropriate (RBC stations will use SM192/716 or SM4M/16M).
- Select the COM port (COM1 probably) and select Via Datalogger, then select the datalogger model (if asked).
- Click `Connect`, and some information should appear in the StatusBox at the right.
- Download the module's stored data using the "Data" tab, putting the data in a new file.
- Erase and test the module using the "Erase" tab (should be pretty self explanatory).
- Be sure to mark the last time the module was erased/tested on a piece of tape attached to the module.`

### Uploading a program to a storage module, then to a datalogger in the field

- Connect a storage module as in steps 1-6 above
- Select Programs tab
- Use store button to place a program in one of the program locations (8 in an SM192).
- Disconnect module, and make a note of where the program is located
- **In the field** connect the storage module to the SC12 cable and then attach the CR10KD keypad to the other end of the cable.
- Use the program transfer mode (*D) to transfer programs. On the CR10D keypad press (treat A like enter?):
  - `*D` - Enter *D Mode
  - `7XA` -  Address Storage Module X (1-8 - in our case there is only one module, so use 1)
  - `1YA` - Save Program in Storage Module as Y (Y=1..8 - the location where the program is/was stored)
  - `2YA`  - Load Program Y from Storage Module
  - `3YA`  - Erase Program Y from Storage Module`

### Setting the clock

- `*5` - Enter clock mode
- `AXXXXA` - Advance to year, then enter year (XXXX), save with A.
- `AYYYA` - Advance to day of year, enter doy (YYY), save with A.
- `AHHMMA` - Advance to time, enter hours and minutes(HHMM), save with A.
- `*0` - Back to status mode.

## Preventing data loss

### Power outages

CR10 dataloggers lose all stored data and programs when they power off
because they do not have battery-backed memory (or power-free memory)
like later dataloggers. This means that a new program will need to be
loaded following a power outage. When powering up, the datalogger looks
for an attached storage module, and will automatically load and run a
program from storage module location 8 if it exists. So, when storage
modules are swapped out, it pays to have the logger program loaded in
location 8 of the replacement module.

**Load programs into storage module locations using the Loggernet SMS utility.**

