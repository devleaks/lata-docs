
LATA can be used as an external application through the lata-cli client application.

The client application makes direct use of the API. Both use the same parameters.

When used from outside of X-Plane, as an external application, LATA has some constraints. It does not connect to X-Plane, so it is necessary to restart LST if it is running so that it sees the newly created files.

# Turnaround

# Taxi

# Tow

# Random Movements

## Random Turnaround

## Random Taxi

## Random Tow


# Cleanup

```
lata-cli cleanup EBBR
```

# Linting Configuration Files

LATA includes a basic linter to cross-check configuration files.

> [!NOTE]
> Simply put, a linter is a tool that programmatically scans your code with the goal of finding issues that can lead to bugs or inconsistencies with code health, data and style. 

```
lata-cli lint
```

The linter includes a gross *object library checker* that scans X-Plane library files and tries to locate object files. If LATA references an object (vehicle or aircraft) and its model cannot be found, the library check will issue a warning. Please recall that the library checker only checks library.txt files and does not locate private library objects not referenced in library files.

