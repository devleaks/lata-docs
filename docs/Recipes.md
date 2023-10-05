Everybody likes cookie.

# Train of vehicle

Baggage vehicle with three wagons, ULD trains with palettes…

```yaml
baggage-train:
  service: baggage
  model:
    - lata/gse/small_baggage_train_tractor.obj
    - lata/gse/small_baggage_train_wagon.obj
    - lata/gse/small_baggage_train_wagon.obj
    - lata/gse/small_baggage_train_wagon.obj
  slow: 5
  speed: 15
  fast: 25
```

# Service with two positions

Example: Refueling under both left and right wings.

```yaml
  - service: fuel
    vehicle: hydrant
    start: -55
    duration: 25
    precise-position: fuel-left
  - service: fuel
    vehicle: hydrant
    start: -58
    duration: 26
    precise-position: fuel-right   
```

# Objects with no movement

If a service has an attribute

```yaml
cones:
  service: aircraft
  model: lata/gse/cone.obj
  slow: 0
  speed: 0
  fast: 0
```


```yaml
  - service: aircraft
    vehicle: cones
    start: 3
    duration: 80
    no-movement: true
```

LATA will not generate any movement for that Service. The object will be spawned at the time of service (`start`) and removed after the service (`duration`).
Typical example of such objects that appear around the aircraft when it arrives are cones or chocks. They are removed, or disappear, just before the aircraft leaves.
