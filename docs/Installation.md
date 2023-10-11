
## Installation Requirements

LATA is an application written in the python language. It will require a working copy of a recent python interpreter.

## LATA Software Installation

Download the latest version of LATA from [GitHub](https://github.com/devleaks/lata). 

Decompress the archive file into X-Plane Custom Scenery folder.

LATA is written in the python langage. 
You will need a python interpreter to run it.
Before you can use the interpreter, you need to install a few python packages. Most people use the pip python package installer.

```sh
$ python --version
Python 3.11.5
$ pip install pyturf networkx ruamel.yaml tabulate
```

The following optional packages can be installed for development or testing purposes:

```sh
$ pip install coloredlogs geojsonio
```

## Custom Library of Objects

LATA includes one default object, a marshall car, the same LiveTraffic plugin uses. If all your aircrafts and ground vehicles appear as marshall cars, you probably did not install [MisterX Library and Aircraft Extension](https://forums.x-plane.org/index.php?/files/file/28167-misterx-library-and-static-aircraft-extension/). LATA examples use this library as it contains both static aircrafts and a variety of ground support vehicles.
## Use as a X-Plane Plugin

Currently, LATA cannot be used as a X-Plane plugin. It must be used from *outside* X-Plane, as a external, independent application.

In a later release, LATA will be accessible directly inside X-Plane.

# lata-cli Application

LATA provides a standalone command-line application to run it.

## Running The Client Application

```sh
$ cd X-Plane/Custom Scenery
$ cd lata/plugins/PythonPlugins/lata
$ python lata-cli.py -h
usage: lata-cli [-h] {help,?,create,clean,lint} ...

positional arguments:
  {help,?,create,clean,lint}
    help (?)            help, print this help
    create              create turnaround, taxi, or tow, or random movement
    clean               clean airport movements or all
    lint                lint configuration files

options:
  -h, --help            show this help message and exit

$ python lata-cli.py create turnaround -h
usage: lata-cli create turnaround [-h] [--add_aircraft | --no-add_aircraft] airport {departure,arrival} [{pax,cargo}] aircraft ramp time

positional arguments:
  airport               ICAO airport code
  {departure,arrival}   Arrival or departure flight
  {pax,cargo}           Passenger flight or cargo
  aircraft              ICAO aicraft type code
  ramp                  Airport ramp name
  time                  date and time of aircraft block time, time should be in ISO format: 2023-10-06T18:00:46 in simulator time zone

options:
  -h, --help            show this help message and exit
  --add_aircraft, --no-add_aircraft
                        Add aircraft object on ramp

$ python lata-cli.py create turnaround LFBO arrival pax A321 F12 "2023-10-08T00:15"

(
..informative output of the execution..
)
```

LATA creates files for LST in the X-Plane 12/Custom Scenery/LATA folder.

```sh

$ ls X-Plane/Custom Scenery/Lata
library
LICENSE
LST_LFBO_TAR_ARR_F12_A321_2310080015
README.md
packages.lst
plugins
```

Now start X-Plane and enjoy *live* turnaround operations on ramps next to you.