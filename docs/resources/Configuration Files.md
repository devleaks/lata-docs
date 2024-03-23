LATA uses a set of configuration files. All files are **Yaml** formatted.

- [[Aircraft Type]] and service equipment position profile (1 file per aircraft),
- [[Ground Support Equipment]] (1 file with all equipments), 
- [[Turnaround Profile]] (1 file per turnaround profile, at least one needed).

# Fields Must Match

Configuration files are very loose and permissive. However, when building activity, a few fields must match.

In case no match is found, the movement is abandoned with warning messages written to screen or log files.

## Service

The type of Service (catering, fuel, apu…) must match in all file. The string used can be anything, it could be `dummy`, however, the word `dummy` must be the service type in the turnaround profile, in the ground support equipment definition (with the 3D model, and the GSE profile. If there is a mismatch, if a turnaround cannot find a Service, or if a service cannot locate a vehicle, warnings will be issued and the Service will be ignored.

## Vehicle

The type of vehicle specified in the Service must match a vehicle type in the ground support equipment definition file. If no vehicle is found, a warning is issued and the service is ignored.

## Service Position

A Service `precise-position` must match the name of a position in the GSE profile. If a precise-position cannot be found, another position for the service is used. If no position can be found, the center of the ramp is used.

# Profile Fallback

For a given aircraft performing a turnaround, there is a sophisticate mechanism to find a suitable profile.
LATA first tries to find a profile for the exact airplane. If none is found it tries to find a profile for an aircraft of the same class. Then for a generic narrow or wide body aircraft, and finally fall back on a large narrow body aircraft (class `C`) which is the default value if none is found.