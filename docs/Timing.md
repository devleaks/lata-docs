When creating a new movement, the creator needs to supply the time at which the movement will occur. Usually, the time that is supplied is the time of arrival or departure from the ramp.

The supplied time is then compared and coordinated with the simulator time (which may not always be the current time).

If the movement is terminated at the simulation time, it is not created. Otherwise, LATA will do its best at synchronizing the movement with the simulator time. Sometimes, only a portion of the movement will be shown.

Synchronisation is performed by requesting Living Scenery Technology (LST) to wait for a precise *day of the year* and *time of the day* before starting the movement.

When LATA generates files for LST, LST need to be restarted to take new files into account. When files are generated outside of X-Plane (i.e. not through a plugin but rather through an external application), LST must be restarted in the simulator after the file have been regerated.