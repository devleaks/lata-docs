Movements contain some randomisation.
# Non Controllable Randomisation
For each ground support vehicle arriving at a ramp, it is not possible to decide where the vehicle is coming from. It will always come from a X-Plane so-called *parking* position.

It is not possible to decide where the vehicle will go after service. It will always go to a X-Plane so-called *destination* position.

Parkings and destinations are special points on the X-Plane airport. X-Plane uses these positions to randomly create ground movements.

Parkings and destinations have an X-Plane *type* like baggage_loader, baggage_train, crew_car, crew_ferrari, crew_limo, pushback, fuel_liners, fuel_jets, fuel_props, food, gpu. These types are converted to LATA service types so that these parking and destination positions are typed according to X-Plane use if a correspondance can be made.

|X-Plane|Service|Vehicle|
|-|-|-|
|baggage_loader|Baggage|belt|
|baggage_train|Baggage|baggage-medium|
|crew_car|Crew|coach-car|
|crew_ferrari|Crew|coach-car|
|crew_limo|Crew|coach-bus|
|pushback|Aircraft|pushback|
|fuel_liners|Fuel|hydrant|
|fuel_jets|Fuel|tanker-large|
|fuel_props|Fuel|tznker-medium|
|food|Catering|catering|
|gpu|Aircraft|gpu|

LATA is not specific to a precise *vehicle type*, but rather to all vehicles of a type of *service*. An X-Plane parking or destination that accepts `fuel_liners` will accept all `fuel` service vehicles in LATA.

# Controllable Randomisation

## Tip and Tricks for Realistic Randomisation

It is not possible to use randomisation without a few constrains. For example, if the parking is randomly selected, one day or another, LATA will select the same parking twice and aircrafts and ground support vehicle will collide. The trick is to exclude random values that have already been used from new generated ones.

