# nettraffic
Prints a one-line network traffic on standard output

## How to use
To get started, simply grant a permission to execute the file, and you can run it anywhere via command line.

    Usage: nettraffic [OPTION]
    Options:
      -i  (%ifname%)      Specify which network interface to monitor. Required.
      -a  (up|dn|total)   Shows which data to display. Prints both if not used.
      -u  (K|KB|M|MB)     Units to show the data in. Automatic if not specified.
      -b                  Show in bits per second (kbps, mbps - small b).
      -e  (0|1|2|3|4|5)   Level of units displayed. (0 for none, 1 for K, 2 for KB, 3 for K/s, 4 for Kb/s, 5 for KB/s). Default of 5.
      -l                  Choose whether or not to display the label (up or down).
      -s  (%string%)      A separator to divide between up and down. Default is none.
      -U  (%string%)      The label for upstream data traffic. Default is up if -l is used.
      -D  (%string%)      The label for downstream data traffic. Default is dn if -l is used.
      -t  (%integer%)     Set the interval for the data update. Default is 1.
      -v                  Prints version number.
      -h                  Prints help.
    
## Example
**Using the minimum requirements**

    $ nettraffic -i wlp2s0
---

    0.0B/s 0.0B/s
    0.7KB/s 0.2KB/s
    53.0KB/s 13.6KB/s

**Displaying total data stream instead of individual up and down**

    $ nettraffic -i wlp2s0 -a total -u K
---

    0.0KB/s
    73.4KB/s
    32.5KB/s

**Using labels and separator**

    $ nettraffic -i wlp2s0 -l -s "|"
---

    0.0B/s dn | 0.0B/s up
    56.7KB/s dn | 32.2KB/s up
    0.2MB/s dn | 0.0MB/s up

**Using custom labels**

    $ nettraffic -i wlp2s0 -l -D " ^" -U " v"
---

    0.0B/s ^ 0.0B/s v
    78.1KB/s ^ 11.4KB/s v
    0.1MB/s ^ 0.1MB/s v
    
**Using custom interval**

    $ nettraffic -i wlp2s0 -t 3
---

    will essentially display the traffic every 3 seconds

**Using different unit levels**

    $ nettraffic -i wlp2s0 -u K -e 1
---

    0.0K 0.0K
    12.1K 11.4K
    114.9K 21.0K

**Using different unit levels (another example)**

    $ nettraffic -i wlp2s0 -a dn -e 3 -l -D " down"
---

    0.0B/s down
    43.2KB/s down
    0.3MB/s down

**Simplest output**

    $ nettraffic -i wlp2s0 -a up -e 1
---

    0.0B
    53.5KB
    0.2MB

## Using it for [polybar](https://github.com/jaagr/polybar/)

**Display both up and down traffic**

    [module/nettraf]
    type = custom/script
    exec = nettraffic -i wlp2s0 -l -U  -D 
    tail = true
    interval = 1
    format = <label>
    label = %output%

**Display traffic separately**

    [module/ntrf]
    type = custom/script
    tail = true
    interval = 1
    format = <label>
    label = %output%

    [module/ntdn_text]
    inherit = module/ntrf
    exec = nettraffic -i wlp2s0 -a dn -e 1

    [module/ntup_text]
    inherit = module/ntrf
    exec = nettraffic -i wlp2s0 -a up -e 1

## Changelog

### 20170118
* Added level of units displayed. 0 for none, 1 for K or M, 2 for KB or MB, 3 for K/s or M/s, and 4 for KB/s or MB/s
* Removed space between value and unit
* Reduced threshold for automatic unit
* Modified help (-h)

### 20170101

* Added option to use custom interval (-t <seconds>)
* Added in-line help (-h)
* Added version number as well as a flag to display it (-v)
* Changed the default threshold for auto unit/suffix
* The script will now be executed in /bin/sh instead of /bin/bash

### 20161224

* Initial Release 
