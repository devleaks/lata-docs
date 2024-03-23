
LATA can be used as an external application through the lata-cli client application.

The client application makes direct use of the API. Both use the same parameters.

When used from outside of X-Plane, as an external application, LATA has some constraints.
1. If LATA is not installed at the recommended location, it needs to know the folder where X-Plane is installed.
2. It does not connect to X-Plane, so it is necessary to restart LST from inside X-Plane so that it takes into account the newly created files.
3. If run from another python installation or environment, required python packages need to be installed in that environment.

Client application accepts `-h` or `--help` flag to provide general help or help specific to an operation.

```sh
$ lata-cli -h                  

usage: lata-cli [-h] {help,?,create,clean,lint} ...

positional arguments:
  {help,?,create,clean,lint,list}
    help (?)            help, print this help
    create              create turnaround, taxi, tow, or random movement
    clean               clean all movements on an airport
    lint                lint configuration files
    list                list possible and valid values for most elements (runways, ramps, aircraft types…)

options:
  -h, --help            show this help message and exit
```


# Turnaround

```sh
$ python lata-cli.py create turnaround -h

usage: lata-cli create turnaround [-h] [--add_aircraft | --no-add_aircraft] airport {departure,arrival} [{pax,cargo}] aircraft ramp time

positional arguments:
  airport               ICAO airport code
  {departure,arrival}   Arrival or departure flight
  {pax,cargo}           Passenger flight or cargo
  aircraft              ICAO aicraft type code
  ramp                  Airport ramp name
  time                  date and time of aircraft block time, time should be in ISO format: 2023-10-08T10:19:38 in simulator time zone

options:
  -h, --help            show this help message and exit
  --add_aircraft, --no-add_aircraft
                        Add aircraft object on ramp

$ python lata-cli.py create turnaround OTHH arrival pax A35K A7 2023-10-08T00:15

```

The arrival or departure flag determines which operations get carried out. The passenger or cargo flag also. (There is no catering on a cargo flight, there more ULD loaders on cargo flights, etc.)
# Taxi

```sh
$ python lata-cli.py create taxi -h      

usage: lata-cli create taxi [-h] airport {departure,arrival} aircraft runway ramp time  

positional arguments:
  airport              ICAO airport code
  {departure,arrival}  Arrival or departure flight
  aircraft             ICAO aicraft type code
  runway               Airport runway for arrival or departure
  ramp                 Airport ramp name
  time                 date and time of aircraft block time, time should be in ISO format: 2023-10-08T10:20:12 in simulator time zone

options:

  -h, --help           show this help message and exit

$ python lata-cli.py create taxi EBBR arrival 02 58L 2023-10-08T00:15

```

# Tow

```sh
$ python lata-cli.py create tow -h       

usage: lata-cli create tow [-h] airport aircraft ramp_from ramp_to [time ...]

positional arguments:
  airport     ICAO airport code
  aircraft    ICAO aicraft type code
  ramp_from   Airport ramp name where aircraft is parked
  ramp_to     Airport ramp name where aicraft will be towed to
  time        date and time of start of tow, time should be in ISO format: 2023-10-08T10:24:39 in simulator time zone

options:
  -h, --help  show this help message and exit

$ python lata-cli.py create tow EDDF A14 C12 now
```

# Random Movements


```sh
$ usage: lata-cli create random [-h] [--continuous | --no-continuous] {turnaround,taxi,tow,trip} [{departure,arrival}] [{pax,cargo}] airport

positional arguments:
  {turnaround,taxi,tow,trip}
                        Type of movement to create
  {departure,arrival}   Arrival or departure flight
  {pax,cargo}           Passenger flight or cargo
  airport               ICAO airport code

options:
  -h, --help            show this help message and exit
  --continuous, --no-continuous
                        Applies to trip only, create continuous loop trip or just once

$ python lata-cli.py create random turnaround EDDM
```

## Random Turnaround

```sh
$ python lata-cli.py create random turnaround EDDM
```

When no time is specified, the movement will start immediately with the taxi-in movement of the aircraft from the runway to the gate (arrival on-block). Turnaround operations will then be synchronized based on the time of arrival of the aircraft at the gate.

## Random Taxi

```sh
$ python lata-cli.py create random taxi EDDM
```

## Random Tow

```sh
$ python lata-cli.py create random tow EDDM
```

# Cleanup

This command removes all files generated for the supplied airport. If there are many generated LST files, airport activity can become busy. To remove all activities at once, issue:

```
lata-cli cleanup EBBR
```

# Linting Configuration Files

LATA includes a basic linter to cross-check configuration files.

> [!NOTE]
> Simply put, a linter is a tool that programmatically scans your code with the goal of finding issues that can lead to bugs or inconsistencies with code health, data and style. 

```
lata-cli lint EBBR
```

The linter includes a gross *object library checker* that scans X-Plane library files and tries to locate object files. If LATA references an object (vehicle or aircraft) and its model cannot be found, the library check will issue a warning. Please recall that the library checker only checks library.txt files and does not search private library objects not referenced in library files.

# Listing Valid Values

```sh
$ lata-cli list EBBR
```

will list all valid values for runways,  ramps, vehicles, aircraft types with model, and turn around services.