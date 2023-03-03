# Autooff

Shutdown or restart when conditions are met.

Made by dotpointer in Bash.

## How it works

The scripts runs a set of scripts in the checks/ directory.
If all of the scripts return a zero return code, then the shutdown continue.
Otherwise it will halt the shutdown.

## List of files

autooff - Main script
LICENSE - License
README.md - This file
checks/001-uptime - Uptime check, at least 30 minutes uptime required
checks/002-users - User check, no logged in users are allowed
checks/003-processes - Processes check, ensure no important processes runs
checks/004-samba - Samba check, no open shares are allowed
checks/005-zfs - ZFS check, no running scrubs are allowed

/etc/dptools/autooff - Main configuration
/etc/dptools/autooff.processes - Processes configuration

/var/log/autooff - Log
/var/cache/autooff - Cache, contains timestamp of last stopped attempt

## Getting Started

These instructions will get you a copy of the project up and running on your
local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them

```
- Debian Linux 11 or similar system
```

### Installing

Head to the /opt directory and clone the repository:

```
sudo mkdir -p /opt
cd /opt
sudo git clone https://gitlab.com/dotpointer/autooff.git
cd autooff/
```

A general configuration file can be added to:
```
/etc/dptools/autooff
```

Example of configuration:
```
#!/bin/bash

# set the cache file location
CACHE="/var/cache/autooff";
# set the log file location
LOG="/var/log/autooff";
# set the log level
LOGLEVEL=2;
# set the minimum allowed timeout between retries
RETRYTIMEOUT=300;
VERBOSE=0;
# set the minimum allowed uptime, export is used because it is a check file
export UPTIMELIMIT=900;
```

A configuration file for processes can be added to:
```
/etc/dptools/autooff
```

Example of processes configuration:
```
#!/bin/bash
GREP="firefox-bin";
grep_process;

GREP="kate";
grep_process;
```

## Usage

Run autooff, either directly or through a cron job. Run with the -h argument to show options and -c to run the checks and output the results.

A log file is written to the following location by default:
```
/var/log/autooff
```

## Authors

* **Robert Klebe** - *Development* - [dotpointer](https://gitlab.com/dotpointer)

See also the list of
[contributors](https://gitlab.com/dotpointer/autooff/contributors)
who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md)
file for details.

Contains dependency files that may be licensed under their own respective
licenses.
