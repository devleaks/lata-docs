LATA uses a set of configuration files. All files are **Yaml** formatted.

- Aircraft types and service equipment profile,
- Ground support equipment,
- Turnaround profile.
# Aircraft Type

```yaml
A321:
  model: lata/aircraft/a321.obj
  class: C
  body: wide
  payload: pax
  wingspan: 31.5
  length: 33.6
```

## Ground Support Equipment Profile
For a given aircraft type, the purpose of the ground support profile is to specify very precise points where ground support vehicule must stop around the aircraft.
Each precise position is given relative to the tip nose of the aircraft.


```yaml
aircraft: A320
…
positions:
    sewage-position:
      service: sewage
      position:
        - 35
        - 2
        - 80
    cleaning:
      - 30
      - 25
      - 0
    catering:
      - 32
      - 5
      - -90
```

For example: Sewage truck will stop 35 meters from the nose tip of the aircraft, 2 meters right from the middle longitudinal axis of the aircraft, and will point 80 degrees (right) from the aircraft axis. The name of that position is `sewage-position`. This position is at the back of a typical small aircraft. If a fourth position is given, it is used to control the height of the contact between the ground support vehicle and the aircraft (bridges, loading belts…)

Distances are in meters, and can be negative, which correspond to the opposite direction. Laterally, left is negative, longitudinally, in front of the aircraft is negative.

Without a precise position of support vehicle through a profile, LATA will use a default profile based on the aircraft class. The default fallback class is class `C`, which correspond to an Airbus A320 or a Boeing 737. To identify profile for an aircraft class, the name of the aircraft type need to be the single letter of the class.

```yaml
aircraft: C
…
```

# Ground Support Equipment


```yaml
small-train:
  service: baggage
  model:
    - lata/gse/small_baggage_train_loco.obj
    - lata/gse/small_baggage_train_wagon.obj
  Lag: 0.4
  slow: 5
  speed: 20
  fast: 30```

### Key
The key is the name of the model of service vehicle (example above: `small-train`).
Please note that in the example above, the model correspond to a set of more than one object chained together, one after the other, each after a `lag` distance.

### Service
Type of the service this vehicle is used for. This criteria is used when selecting a vehicle for a service.

### Model
X-Plane virtual path to 3D model file.
The model is searched in all libraries available to X-Plane.
(The demo only uses standard X-Plane models.)

### Slow, Speed, and Fast
The three attributes are the speed of movement in kilometres per hour for the vehicle. Fast is the speed on service roads. Normal is the speed on ramps. Slow is the speed when closing to the aircraft.

# Turnaround Profile
The turnaround profile is a set of individual services.
The profile first starts with a few selective attributes, and if followed by one or more services.

## Profile Attributes

### Aircraft type
ICAO Aircraft type.
The aircraft type can also be an aircraft class, a single letter `A` to `F`, which characterise all aircrafts of that class.

### Movement
Determine if the profile applies to arrival or departure.

### Ramp Type
Determine if the profile applies to ramp with a jetway, or parking with jetway.

### Payload
Determine if the aircraft is a passenger (`pax`) or a `cargo` flight.

### Services
The list of services for that profile.

## Service
Each service correspond to the move of a ground support equipment that first travels from a *parking* to the ramp, then delivers the service to the aircraft, and finally leaves the ramp to a final *destination*.
Each service is scheduled to occur at a time relative to the movement of the flight.
For arrival services, scheduling of services is relative to the arrival time of the flight which correspond to the on-block time. For departure services, scheduling is relative the departure time of the flight, which correspond to the off-block time.

### Service
Type of the service.
Example of service types are: sewage, catering, refuelling, baggage offloading or loading, cargo handling, water, APU, cones…

### Vehicle
Name of the model of service vehicle used to deliver the service. Must correspond to the model of a Ground Support Equipment above.

### Start
Time in minutes, relative to the block time, when the service should occur.
For example: refuelling, start: -40: Refueling will start 40 minutes before the off-bloxk departure time.

### Duration
Duration time of the service in minutes. For example: refueling, duration: 25. Refueling will last 25 minutes after arrival of the service vehicle next to the aircraft. After 25 minutes, the service vehicle will leave to ramp area to its destination.

### Precise Position
A precise position is the position where the service vehicle should go.

When scheduling several services of the same type, it is possible to precise which position to select to avoid these vehicle to collide at the same position. For example, when scheduling two fuel services, it is possible to send each fuel truck under each wing.

If no service position is specified, LATA will select a position for the service. If no position is found, the center of the ramp is selected.

### No Movement
If a service contains a `no-movement` attribute, LATA will place the vehicle for the corresponding service at the service time but will not animate the vehicle. It will remove the vehicle at the end of the service.

In this case, vehicle should be thought as an « object ». For example, it is possible to place cones or chocks around the aircraft and have them disappear at the end of the turnaround. Cones or chocks will appear and disappear but will not be animated.

### Name
Optional service name. The name is used in comments. If no name is used, LATA will assign a unique name.

# Fields Must Match

Configuration files are very loose and permissive. However, when building activity, a few fields must match.

In case no match is found, the movement is abandoned with warning messages written to screen or log files.

## Service
The type of Service (catering, fuel, apu…) must match in all file. The string used can be anything, it could be `dummy`, however, the word `dummy` must be the service type in the turnaround profile, in the ground support equipment definition (with the 3D model, and the GSE profile. If there is a mismatch, if a turnaround cannot find a Service, or if a service cannot locate a vehicle, warnings will be issued and the Service will be ignored.
## Vehicle
The type of vehicle specified in the Service must match a vehicle type in the ground support equipment definition file. If no vehicle is found, a warning is issued and the service is ignored.
## Service Position
A Service `precise-position` must match the name of a position in the GSE profile. If a precise-position cannot be found, another position for the service is used. If no position can be found, the center of the ramp is used.