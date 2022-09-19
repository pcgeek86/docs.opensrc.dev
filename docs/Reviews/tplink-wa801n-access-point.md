# TP-Link TL-WA801N Access Point

In Q3 2022, I purchased 3x of the [TP-Link TL-WA801N Access Points](https://amzn.to/3UlwepI) to use as client bridge devices.
I needed to extend my network wirelessly, rather than running cables throughout my house and property.

I have a number of different security cameras that require wired connections, and don't have built-in wireless capabilities.
These cameras offer excellent image quality, and are inexpensive, hence why I am okay with them not having wireless.
I also have some workstations that do not have wireless network interfaces available on them, hence I need to hardwire them.

Rather than plugging a device directly into each of the TL-WA801N devices, I plugged each of them into to an unmanaged [TP-Link TL-SG108 8-port network switch](https://amzn.to/3BRR9JM).
That way, I can use the TL-WA801N as a bridge for multiple devices, not just a single device.

## Performance

The performance of the TL-WA801N is subpar overall.
To test performance of this access point, I installed `iperf3` onto an ODROID M1 that was plugged into the network switch, connected via the TL-WA801N.
Then I ran `iperf3 --server`, and attempted to access the `iperf3 --client <ip-address>` from my desktop workstation.
My desktop workstation, the `iperf3` client, has a [TP-Link AC1300 USB wifi adapter](https://amzn.to/3SkTnqJ).

### Benchmark Results

Here's the raw output from a single run of `iper3` on my desktop workstation, to my ODROID M1.
As you can see, performance is sitting around 60 megabits per second, which is far, far below the advertised 300 Mbps.

```
Connecting to host <hostname>.local, port 5201
[  4] local fe80::xxxxxxxx port 52319 connected to fe80::xxxxxxx port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  6.75 MBytes  56.6 Mbits/sec
[  4]   1.00-2.00   sec  7.25 MBytes  60.8 Mbits/sec
[  4]   2.00-3.00   sec  7.88 MBytes  66.0 Mbits/sec
[  4]   3.00-4.00   sec  7.12 MBytes  59.8 Mbits/sec
[  4]   4.00-5.00   sec  7.75 MBytes  64.9 Mbits/sec
[  4]   5.00-6.00   sec  8.25 MBytes  69.3 Mbits/sec
[  4]   6.00-7.00   sec  7.38 MBytes  61.8 Mbits/sec
[  4]   7.00-8.00   sec  7.38 MBytes  61.9 Mbits/sec
[  4]   8.00-9.00   sec  7.12 MBytes  59.8 Mbits/sec
[  4]   9.00-10.00  sec  8.00 MBytes  67.1 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  74.9 MBytes  62.8 Mbits/sec                  sender
[  4]   0.00-10.00  sec  74.9 MBytes  62.8 Mbits/sec                  receiver

iperf Done.
```

I ran another test in the reverse direction, just to see if anything would change.
The results are substantially similar, given an equivalent network environment.
This should be pretty obvious, considering that the `iperf3` test is already going in both directions.
The only difference is that I'm switching which device is initiating the connection.

```
Connecting to host xxxxxx.local, port 5201
[  5] local xxxxxx port 40836 connected to xxxxxxxxx port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  6.88 MBytes  57.7 Mbits/sec   14   85.9 KBytes
[  5]   1.00-2.00   sec  6.87 MBytes  57.6 Mbits/sec    5   93.9 KBytes
[  5]   2.00-3.00   sec  6.63 MBytes  55.6 Mbits/sec    2    105 KBytes
[  5]   3.00-4.00   sec  7.78 MBytes  65.2 Mbits/sec    8    110 KBytes
[  5]   4.00-5.00   sec  6.87 MBytes  57.6 Mbits/sec    6    102 KBytes
[  5]   5.00-6.00   sec  7.41 MBytes  62.2 Mbits/sec    2    110 KBytes
[  5]   6.00-7.00   sec  6.93 MBytes  58.1 Mbits/sec    3    118 KBytes
[  5]   7.00-8.00   sec  7.29 MBytes  61.2 Mbits/sec    8   85.9 KBytes
[  5]   8.00-9.00   sec  6.99 MBytes  58.7 Mbits/sec    2    102 KBytes
[  5]   9.00-10.00  sec  8.08 MBytes  67.8 Mbits/sec    7   77.8 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  71.7 MBytes  60.2 Mbits/sec   57             sender
[  5]   0.00-10.00  sec  71.4 MBytes  59.9 Mbits/sec                  receiver
```

## Issues

### Power Outage Recovery

One of the biggest issues I noticed with the TL-WA801N is that they don't automatically recover from power outages.
It's possible that the issue is related to the Power-over-Ethernet (PoE) adapter that they include, however I am not sure.
At the time of a power outage, I had two TL-WA801N devices plugged in. 
Neither of them were powered on when I checked on them; all three lights on both devices were **off**.

As soon as I unplugged each device, and plugged the network cable back in, power and connectivity was restored.
I am not thrilled that there is manual effort required to recover from a power outage.
I am hopeful that the AC1200 model will not exhibit the same power problems as the N300 TL-WA801N.