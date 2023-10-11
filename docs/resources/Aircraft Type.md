
Aircraft type it used for two main informations. The overall size of the aircraft for determining average turn around operation times, but also to determine the precise position of ground support vehicle around the aircraft. The later is called the Ground Support Equipment Profile.

```yaml
aircraft: A321
icao: A321
iata: 321,32S
mtow: 83000
wingspan: 34.1
length: 44.51
height: 11.76
equivalences:
- '321'
- 32S
- A21N
class: B
model: XCSL_AIRCRAFTS/A321fCFM.AIB2.xpmp2.obj
liveries:
  - A321_AAR.obj
  - A321_ACA.obj
positions:
  sewage:
    service: sewage
    position:
      - 35
      - 0
      - 90
  cleaning:
    service: cleaning
    position:
      - 30
      - 25
      - 0
  catering:
    service: catering
    position:
      - 32
      - 5
      - -90
  fuel:
    service: fuel
    position:
      - 15
      - 10
      - 90
  fuel2:
    service: fuel
    position:
      - 15
      - -10
      - -90
```

## Ground Support Equipment Profile

For a given aircraft type, the purpose of the ground support equipment profile is to specify very precise points where ground support vehicle must stop around the aircraft.

![[aircraft_ramp.png]]

Each precise position is given relative to the tip nose of the aircraft.

![[service_positions.png]]

```yaml
aircraft: A320
…
positions:
  sewage:
    service: sewage
    position:
      - 35
      - 0
      - 80
  cleaning:
    service: cleaning
    position:
      - 30
      - 25
      - [70, 110]
  catering:
    service: catering
    position:
      - 32
      - 5
      - -90
    backup: true

```

For example: Sewage truck will stop 35 meters from the nose tip of the aircraft, 2 meters right from the middle longitudinal axis of the aircraft, and will point 80 degrees (right) from the aircraft axis. The name of that position is `sewage-position`. This position is at the back of a typical small aircraft. If a fourth position is given, it is used to control the height of the contact point between the ground support vehicle and the aircraft (bridges, loading belts…) if needed.

Distances are in meters, and can be negative, which correspond to the same distance in the opposite direction. Laterally, left is negative, longitudinally, in front of the aircraft is negative.

If the value is a list of 2 values, a random value is taken within the range of values. Example above is orientation of cleaning truck between `[70, 110]` range.

If `backup` is set to true, the vehicle will first backup from its service position and then leave.

Without a precise position of support vehicle through a profile, LATA will use a default profile based on the aircraft class. The default fallback class is class `C`, which correspond to an Airbus A320 or a Boeing 737. To identify profile for an aircraft class, the name of the aircraft type need to be the single letter of the class. The aircraft name needs to be the same as the aircraft class.

```yaml
aircraft: C
	class: C
…
```

