# Autooff

A script to shutdown the system when certain conditions are met.

Made by dotpointer in Bash.

## How it works

The scripts runs a set of scripts in the stoppers/ directory.
If all of the scripts return a zero return code, then the shutdown continue.
Otherwise it will halt the shutdown.

## List of files

autooff - Main script
LICENSE - License
README.md - This file
stoppers/001-uptime - Uptime check, at least 30 minutes uptime required
stoppers/002-users - User check, no logged in users are allowed
stoppers/003-processes - Processes check, ensure no important processes runs
stoppers/004-samba - Samba check, no open shares are allowed

## Getting Started

These instructions will get you a copy of the project up and running on your
local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them

```
- Debian Linux 9 or similar system
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
LOG="/tmp/log";
LOGLEVEL=2;
VERBOSE=0;
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

Run autooff, either directly or through a cron job. Run with the -h argument to show options.

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
