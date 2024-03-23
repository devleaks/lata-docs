
# Parameters

## XPLANE_BASE
Home directory of X-Plane.

LATA uses the folder to find X-Plane files like airport definitions and objects.

If LATA was not installed in the X-Plane Custom Scenery folder, LATA will create a Custom Scenery called LATA and will place its generated files in that directory for LST. On restart, LST will automagically find those new files and generate traffic accordingly.

> If you installed LATA in X-Plane Custom Scenery folder, there is no need to specify this parameter.

# Options

## Exclude Runways from Taxiways
Boolean, explicit.

## Cargo Flight Percentage
Value between 0 and 100, to specify the ratio of passenger and cargo flights.
When a flight is randomly generated, this parameter drives the type of the flight.
Setting the cargo flight percentage to 25 will generate 75% passenger flights and 25% cargo flights.

## Closest Destination
When picking up parking and destination for service vehicle, this flag indicates whether the parking and/or destination that is closest to the ramp should be chosen. Otherwise a random remote parking might be chosen.
It is advisable, for realistic turnaround operations, to enforce this flag, especially for cargo flights.