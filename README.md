# nettraffic
Prints a one-line network traffic on standard output

## How to use
To get started, simply grant a permission to execute the file, and you can run it anywhere via command line.

    Usage: nettraffic [OPTION]
    Options:
      -i  (%ifname%)          Specify which network interface to monitor. Required.
      -a  (up|dn|down|total)  Shows which data to display. Displays both up and down if not specified.
      -u  (K|KB|M|MB)         Units to show the data in. Will automatically round to the closest unit if not specified.
      -l  *no arguments*      Choose whether or not to display the label (up or down). Will not display if not used.
      -s                      A separator to divide between up and down. Will not use a separator if not specified.
      -U                      The label for upstream data traffic. Default is 'up' if -l is used.
      -D                      The label for downstream data traffic. Default is 'dn' if -l is used.
      
## Example
Using the minimum requirements

    $ nettraffic -i wlp2s0
---

    0.0 B/s 0.0 B/s
    0.7 KB/s 0.2 KB/s
    53.0 KB/s 13.6 KB/s

Displaying total data stream instead of individual up and down

    $ nettraffic -i wlp2s0 -a total -u K
---

    0.0 KB/s
    73.4 KB/s
    32.5 KB/s

Using labels and separator

    $ nettraffic -i wlp2s0 -l -s "|"
---

    0.0 B/s dn | 0.0 B/s up
    156.7 KB/s dn | 32.2 KB/s up
    211.0 KB/s dn | 24.8 KB/s up

Using custom labels

    $ nettraffic -i wlp2s0 -l -D "^" -U "v"
---

    0.0 B/s ^ 0.0 B/s v
    78.1 KB/s ^ 11.4 KB/s v
    114.9 KB/s ^ 21.0 KB/s v
