# Redis Sniffer v1.1.1
[![PyPI version](https://badge.fury.io/py/redis-sniffer.svg)](http://badge.fury.io/py/redis-sniffer) [![License](http://img.shields.io/:license-mit-blue.svg)](http://jplesperance.mit-license.org) [![Requirements Status](https://requires.io/github/jplesperance/redis-sniffer/requirements.svg?branch=bugfix%2FRS-1-allow-capture-of-non-redis-traffic)](https://requires.io/github/jplesperance/redis-sniffer/requirements/?branch=bugfix%2FRS-1-allow-capture-of-non-redis-traffic)  [![Build Status](https://travis-ci.org/jplesperance/redis-sniffer.svg?branch=bugfix%2FRS-1-allow-capture-of-non-redis-traffic)](https://travis-ci.org/jplesperance/redis-sniffer.svg?branch=bugfix%2FRS-1-allow-capture-of-non-redis-traffic) [![Code Climate](https://codeclimate.com/github/jplesperance/redis-sniffer/badges/gpa.svg)](https://codeclimate.com/github/jplesperance/redis-sniffer) [![codecov.io](http://codecov.io/github/jplesperance/redis-sniffer/coverage.svg?branch=master)](http://codecov.io/github/jplesperance/redis-sniffer?branch=master)

## About

This tool will monitor a specific port and interface for redis traffic and captures the commands being sent to Redis and/or formatted full TCP dump data.  This can be used for analysis for debugging or for replaying the transactions as a way of doing real load/performance testing.

All installation and usage documentation are now located at: https://redis-sniffer.readme.io/docs/getting-started

python3 Install:

pip3 install hiredis

pip3 install pcap

pip3 install pypcap

pip3 install nose

pip3 install codecov

pip3 install dpkt

git clone https://github.com/earl86/redis-sniffer.git

python3 -m pip install redis-sniffer/


redis-sniffer -h

usage: redis-sniffer [-h] 

(-i INTERFACE | -F FILE) 

[-p PORT] 

[--out OUT]

[-l {debug,event,full}] 

[-el EVENT_LOG] 

[-fl FULL_LOG]

[-f FILTER] 

[--append APPEND] 

[--extra EXTRA]


optional arguments:

  -h, --help            show this help message and exit
  
  -i INTERFACE, --interface INTERFACE
                        the interface to bind to
                        
  -F FILE, --file FILE  pcap file containing captured traffic to analyze
  
  -p PORT, --port PORT  the port to grab packets from. Default: 6379
  
  --out OUT             the location to generate the full or event logs,
                        defaults to the directory the application is executed
                        from
                        
  -l {debug,event,full}
                        the type of log(s) you want to create. Default: full
                        
  -el EVENT_LOG, --event-log EVENT_LOG
                        the name of the event outout file. Default:
                        event_sniff
                        
  -fl FULL_LOG, --full-log FULL_LOG
                        the name of the full sniff output file. Default:
                        full_sniff
                        
  -f FILTER, --filter FILTER
                        comma separated list of events to log(ex:
                        setex,delete)
                        
  --append APPEND       the suffix to append to command logs
  
  --extra EXTRA         log non-redis traffic



Usage

You've got it installed, but how to use it.

Suggest Edits

Redis Sniffer binds to a network interface and analyzes the traffic that is crossing the interface on the specified port.

At the most basic level using Redis Sniffer is extremely simple.

Shell

redis-sniffer -i <interface> -p <port>

# example

redis-sniffer -i eth0 -p 6379

This will cause all redis events going across eth0 on port 6379 to be logged. When used without the '--out' flag, Redis Sniffer will log to the current working directory. Below are some examples of other options that can be used and their affect.

Shell

# log all redis traffic on port 6379 crossing bond0 interface and have the logs written to the /var/log/redis-sniffer folder

redis-sniffer -i bond0 -p 6379 --out /var/log/redis-sniffer

# log only select redis commands; -f allows a comma separated list of redis commands to log.  when using the -f flag, each command specified will be logged to a seperate file

redis-sniffer -i bond0 -p 6379 --out /var/log/redis-sniffer -f select

# other options

-l [full,event,debug] - the level of logging, defaults to full

-el, --event-log - The name of the file that redis events are logged to

-fl, --full-log - The name of the file that all traffic is logged to

--append - a suffix to append to the file names from using filters

