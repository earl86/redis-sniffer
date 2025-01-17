# Redis Sniffer v1.1.1 for Python3

## About

This tool will monitor a specific port and interface for redis traffic and captures the commands being sent to Redis and/or formatted full TCP dump data.  This can be used for analysis for debugging or for replaying the transactions as a way of doing real load/performance testing.

# Install
yum install libpcap

yum install libpcap-devel

pip3 install hiredis

pip3 install pypcap

pip3 install nose

pip3 install codecov

pip3 install dpkt

git clone https://github.com/earl86/redis-sniffer.git

python3 -m pip install redis-sniffer/


# Help

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


### optional arguments:

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



# Usage

You've got it installed, but how to use it.

Redis Sniffer binds to a network interface and analyzes the traffic that is crossing the interface on the specified port.

At the most basic level using Redis Sniffer is extremely simple.

redis-sniffer -i [interface] -p [port] --out [/dir/]

# example

redis-sniffer -i eth0 -p 6379

This will cause all redis events going across eth0 on port 6379 to be logged. When used without the '--out' flag, Redis Sniffer will log to the current working directory. Below are some examples of other options that can be used and their affect.


## log all redis traffic on port 6379 crossing bond0 interface and have the logs written to the /var/log/redis-sniffer folder

redis-sniffer -i bond0 -p 6379 --out /var/log/redis-sniffer/

## log only select redis commands; -f allows a comma separated list of redis commands to log.  when using the -f flag, each command specified will be logged to a seperate file

redis-sniffer -i bond0 -p 6379 --out /var/log/redis-sniffer/ -f select


## example result

redis-sniffer -i bond4 -p 6380 --out /tmp/

tail -f event_sniff 

[b'set', b'a', b'1']

[b'set', b'a', b'1']


tail -f full_sniff 

1705049403.276039 10.17.13.2:63901            81       59 [b'set', b'a', b'1']

1705049404.527709 10.17.13.2:63901            81       59 [b'set', b'a', b'1']

