
# Use as a X-Plane Plugin

Currently, LATA cannot be used as a X-Plane plugin. You must use it "externally".


# Setup Parameters

Please edit the file `__init__.py` with a text editor and adjust the path to X-Plane home folder.

# Use lata-cli Application

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

## Running The Client Application

```sh
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

$ python lata-cli.py create turnaround LFBO arrival pax A321 F12 now

(
..informative output of the execution..
)
```

LATA creates files for LST in the X-Plane 12/Custom Sceneries/LATA folder.

```sh

$ ls X-Plane 12/Custom Scenery/Lata
LICENSE
LST_LFBO_TAR_ARR_F12_A321_2310061618
LST_LFBO_TAR_ARR_F12_A321_2310061619
LST_LFBO_TAR_ARR_F12_A321_2310061753
LST_LFBO_TAR_ARR_F12_A321_2310061759
LST_LFBO_TAR_ARR_F12_A321_2310061801
LST_LFBO_TAR_ARR_F12_A321_2310061802
README.md
XCSL_AIRCRAFTS
XCSL_CARS
packages.lst
plugins
```

Now start X-Plane and enjoy *live* turnaround operations on ramps next to you.