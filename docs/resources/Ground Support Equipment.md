
Each piece of equipment need to be declared so that it can be associated with an 3D object, called the model, and reproduced in the simulator.


```yaml

small-train:
  service: baggage
  model:
    - lata/gse/baggage_train_tractor.obj
    - lata/gse/baggage_train_wagon.obj
  lag: 0.4
  slow: 5
  speed: 20
  fast: 30
```

### Key
The key is the name of the type of service vehicle (example above: `small-train`).

### Service
Type of the service this vehicle is capable of delivering. This criteria is used when selecting a vehicle for a service.

### Model
X-Plane virtual path to 3D model file.
The model is searched in all libraries available to X-Plane.
(The demo only uses standard X-Plane models.)

Please note that in the example above, the model correspond to a list of more than one 3D object chained together, one after the other, each after a `lag` distance. The chain of element is called a *train*.

### Slow, Speed, and Fast
The three attributes are the speed of movement in kilometres per hour for the vehicle. Fast is the speed on service roads. Normal is the speed on ramps. Slow is the speed when closing to the aircraft.

> Please note that in LST the speed of an object cannot be zero, in which case the object would stop and no longer progress. Setting speed to 0 is like infinite WAIT.

