Everybody likes cookie.

# Train of vehicle

Baggage vehicle with three wagons, ULD trains with palettes…

# Service with two positions

Example: Refueling under both left and right wings.

# Objects with no movement

If a service has an attribute

```yaml
  no-movement: true
```

LATA will not generate any movement for that Service. The object will be spawned at the time of service (`start`) and removed after the service (`duration`).
Typical example of such objects that appear around the aircraft when it arrives are cones or chocks. They are removed, or disappear, just before the aircraft leaves.
